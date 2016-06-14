### QT Cheatsheet ###

#### QString ####

```c++
QString hello = "Hello, World";
QString text = QString(I have %1 taka!).arg(10);
QString *textPtr = new QString("A Beautiful Text");
qDebug() << hello << "\n";
```
```c++
int number = 10;
QString string = "This a cute string";
QString show = QString("My number is: %1 and my string is: %2\n").arg(number).arg(string);
qDebug() << show;
```

#### QTextStream ####

```c++
QString qstr;
QTextStream cout(stdout);				/* stream text to stdout */
QTextStream cin(stdin);				/* take input from stdin */
QTextStream toStringObject(&qstr);	/* store in a Qstring */

cout << "Hello, world!\n"
cout << QString("First prime number is: %1\n").arg(2);

QString inputString;
cin >> inputString;
cout << inputSting;

toStringObject << "This is a literal string\n" << QString("A QString with number %1\n").arg(10) << inputString << "\n";
cout << qstr;
```

#### Taking Commandline Arguments ####

```c++
#include <QCoreApplication>
#include <QStringList>
#include <QDebug>

int main(int argc, char *argv[]){
	QCoreApplication app(argc, argv);

	QStringList argList = app.arguments();

	foreach(const QString &str, argList){
		qDebug() << str;
	}

	return EXIT_SUCCESS;
}
```

#### Making a basic QT class with signals and slots ####

We will create our own string class base on QString. Our class name will be MyString. All QT classes inherits QObject class as base class. Q_OBJECT macro will be used for signals and slots. Slots are just regular member function. They are called when a signal is emitted. signals are only function prototypes. Their arguments must match with the slots, they are emitted. Slots can be called as regular member function too. In the constructor QObject argument is taken as parent so that others can make QObject as parent for safe memory deallocation.

###### MyString.h ######
```c++
#include <QObject>
#include <QString>

class MyString: public QObject{

    Q_OBJECT

private:
    QString m_text;

public:
    MyString(const QString& text, QObject *parent = 0);

    const QString& text(void) const;
    int getLengthOfText(void) const;

public slots:
    void setText(const QString&);

signals:
    void textChanged(const QString&);
};
```

###### MyString.cpp ######
```c++
#include <QObject>
#include <QString>
#include "MyString.h"

MyString::MyString(const QString& text, QObject *parent)
    : QObject(parent), m_text(text) {}

const QString& MyString::text(void) const {
    return m_text;
}

int MyString::getLengthOfText() const {
    return m_text.size();
}

void MyString::setText(const QString& text){
    if(text == m_text)
        return;

    m_text = text;

    emit textChanged(m_text);
}
```

###### main.cpp ######
```c++
#include <QObject>
#include <QDebug>
#include "MyString.h"

int main(){
    QObject parent;
    MyString *a, *b;

    a = new MyString(QString("Hello, World!"), &parent);
    b = new MyString(QString("I am Bee"), &parent);

    qDebug() << a->text();
    qDebug() << b->text();

    a->setText(QString("a changed so, b will change too"));
    QObject::connect(a, SIGNAL(textChanged(const QString&)), b, SLOT(setText(const QString&)));

    qDebug() << a->text();
    qDebug() << b->text();

    return 0;
}
```

#### Basic QT Dialog with Button, Label and MessageBox ####

Our class ingerits from QDialog. It has to public slots for two buttons.

###### mydialog.h ######
```c++
#ifndef __DIALOG_H__
#define __DIALOG_H__

#include <QDialog>
#include <QObject>

class MyDialog: public QDialog{

    Q_OBJECT

public:
    MyDialog();

public slots:
    void blueClicked();
    void redClicked();
};

#endif
```

###### mydialog.cpp ######
```c++
#include "mydialog.h"
#include <QPushButton>
#include <QHBoxLayout>
#include <QVBoxLayout>
#include <QMessageBox>
#include <QLabel>

MyDialog::MyDialog(){
    resize(300, 400);

    QLabel *label = new QLabel("Select:");

    QPushButton *blue = new QPushButton("Blue Pill");
    QPushButton *red = new QPushButton("Red Pill");

    QHBoxLayout *btnLayout = new QHBoxLayout;
    QHBoxLayout *lblLayout = new QHBoxLayout;

    btnLayout->addWidget(blue);
    btnLayout->addStretch();
    btnLayout->addWidget(red);

    
    lblLayout->addStretch();

    QVBoxLayout *mainLayout = new QVBoxLayout(this);

    mainLayout->addStretch();
    
    mainLayout->addLayout(btnLayout);
    mainLayout->addStretch();

    connect(blue, SIGNAL(clicked()), this, SLOT(blueClicked()));
    connect(red, SIGNAL(clicked()), this, SLOT(redClicked()));
}

void MyDialog::blueClicked(){
    QMessageBox::information(this, "Your Choice", "Welcome to Matrix!");
}

void MyDialog::redClicked(){
    QMessageBox::information(this, "Your Choice", "Good Bye!");
}
```

###### main.cpp ######
```c++
#include <QApplication>
#include "mydialog.h"

int main(int argc, char *argv[]){
    QApplication app(argc, argv);

    MyDialog mdlg;
    mdlg.show();

    return app.exec();
}
```

#### Basic QMainWindow with Central Widget, Menu Bar, Tool Bar ####

###### mywindow.h ####
```c++
#ifndef __MY_WINDOW_H__
#define __MY_WINDOW_H__

#include <QMainWindow>
#include <QOBject>

class QAction;
class QTextEdit;

class MyWindow: public QMainWindow{

    Q_OBJECT

private:
    QAction *actionNew;
    QAction *actionCut;
    QAction *actionAbout;
    QAction *actionClose;

    QTextEdit *editText;

    void setupActions();
    void setupMenu();
    void setupToolBar();

public:
    MyWindow();

public slots:
    void newFile();
    void cut();
};

#endif
```

###### mywindow.cpp ######
```c++
#include <QMainWindow>
#include <QAction>
#include <QString>
#include <QTextEdit>
#include <QAction>
#include <QMenu>
#include <QMenuBar>
#include <QToolBar>
#include <QApplication>
#include "mywindow.h"

MyWindow::MyWindow(){	
	setWindowTitle(QString("Untitled[*]"));

	editText = new QTextEdit(this);	
	
	setCentralWidget(editText);

	connect(editText->document(), SIGNAL(modificationChanged(bool)), this, SLOT(setWindowModified(bool)));

	setupActions();
	setupMenu();
	setupToolBar();
}

void MyWindow::setupActions(){
	actionNew = new QAction(tr("New"), this);
	actionNew->setShortcut(tr("Ctrl+N"));
	actionNew->setStatusTip(tr("Open a new document"));

	connect(actionNew, SIGNAL(triggered()), this, SLOT(newFile()));

	actionCut = new QAction(tr("Cut"), this);
	actionCut->setShortcut(tr("Ctrl+X"));
	actionCut->setStatusTip(tr("Cut"));
	actionCut->setEnabled(false);

	connect(editText, SIGNAL(copyAvailable(bool)), actionCut, SLOT(setEnabled(bool)));
	connect(actionCut, SIGNAL(triggered()), this, SLOT(cut()));

	actionAbout = new QAction(tr("About QT"), this);
	actionAbout->setStatusTip(tr("About QT Toolkit"));

	connect(actionAbout, SIGNAL(triggered()), qApp, SLOT(aboutQt()));

	actionClose = new QAction(tr("&Quit"), this);
	actionClose->setShortcut(tr("Ctrl+Q"));
	actionClose->setStatusTip(tr("Close"));

	connect(actionClose, SIGNAL(triggered()), qApp, SLOT(quit()));
}

void MyWindow::setupMenu(){
	QMenu *fileMenu = menuBar()->addMenu(tr("File"));
	fileMenu->addAction(actionNew);
	fileMenu->addSeparator();
	fileMenu->addAction(actionClose);

	QMenu *editMenu = menuBar()->addMenu(tr("Edit"));
	editMenu->addAction(actionCut);

	QMenu *helpMenu = menuBar()->addMenu(tr("Help"));
	helpMenu->addAction(actionAbout);
}

void MyWindow::setupToolBar(){
	QToolBar *toolBar;
	toolBar = addToolBar(tr("Tool"));

	toolBar->addAction(actionNew);
	toolBar->addSeparator();
	toolBar->addAction(actionCut);
}

void MyWindow::newFile(){

}

void MyWindow::cut(){

}
```

###### main.cpp ######
```c++
#include <QApplication>
#include "mywindow.h"

int main(int argc, char *argv[]){
    QApplication app(argc, argv);

    MyWindow mainwindow;
    mainwindow.show();

    return app.exec();
}
```

#### QList, QStringList, QStringList::iterator, QListIterator<QString> ####

```c++
#include <QStringList>
#include <QDebug>

int main(){
	QString heavy = "Metallica, Stentorian, Aurthohin";
	QString alt = "Icons, Karnival, Nemesis";
	QString symphonic = "Ionic, Eluveitie";

	QStringList bands;
	bands << heavy << alt << symphonic;

	qDebug() << "Heavy: " << bands[0] << "\n";
	qDebug() << "Alt: " << bands[1] << "\n";
	qDebug() << "Symphonic: " << bands[2] << "\n";

	QString allBands = bands.join(", ");
	qDebug() << allBands << "\n";

	QList<QString> singleBandList = allBands.split(", ");
	
	foreach(const QString& str, bands){
		qDebug() << QString("[%1]").arg(str);
	}

	qDebug() << "\n\n";

	for(QStringList::iterator it = bands.begin();
		it != bands.end(); it++){
			qDebug() << QString("[[%1]]").arg(*it);
	}

	qDebug() << "\n";

	QListIterator<QString> it(singleBandList);
	while(it.hasNext()){
		qDebug() << QString("{%1}").arg(it.next());
	}

	return 0;
}
```

#### QDir, QFileInfo, QDirIterator ####

```c++
#include <QCoreApplication>
#include <QStringList>
#include <QDebug>
#include <QDir>

int main(int argc, char *argv[]){
	QCoreApplication app(argc, argv);

	QDir dir = QDir::current();
	if(app.arguments().size() > 1){
		dir = app.arguments()[1];
	}

	dir.setSorting(QDir::Name);
	
	QDir::Filters df = QDir::Files | QDir::NoDotAndDotDot;

	QStringList dirList = dir.entryList(df, QDir::Name);

	foreach(const QString &entry, dirList){
		QFileInfo fileInfo(dir, entry);
		qDebug() << fileInfo.absoluteFilePath();
	}

	return EXIT_SUCCESS;
}
```

```c++
/* Will search all mp3 file in a given directory
 * And its subdirectories
 */

#include <QCoreApplication>
#include <QStringList>
#include <QDebug>
#include <QDir>
#include <QDirIterator>
#include <QTextStream>

int main(int argc, char *argv[]){
	QCoreApplication app(argc, argv);

	QTextStream cout(stdout);
	QTextStream cerr(stderr);

	QDir dir = QDir::current();
	if(app.arguments().size() > 1){
		dir = app.arguments()[1];
	}

	if(!dir.exists()){
		cerr << dir.path() << " doesn't exist!\n";
		return -1;
	}

	QDirIterator qdi(dir.absolutePath(), QStringList() << "*.mp3", QDir::NoSymLinks | QDir::Files, QDirIterator::Subdirectories);
	while(qdi.hasNext()){
		cout << qdi.next() << "\n";
	}

	return EXIT_SUCCESS;
}
```

#### QFile ####

```c++
QFile file("myTextFile.txt");
file.open(QIODevice::WriteOnly);

QTextStream outFile(&file);
outFile << "Hello, World!" << "\n";

file.close();
```

```c++
QFile file("myTextFile.txt");
if(file.open(QIODevice::ReadOnly)){
	QStringSteam inFile(&file);
	QString text;

	inFile >> text;
	qDebug() << text;
}
```

#### QDate ####

`QDate::currentDate()` returns current date

 
QDialog
QInputDialog
QFileDialog
QMessageBox
