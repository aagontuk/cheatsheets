### QT Cheatsheet ###

#### Index ####

1. [QString](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qstring)
2. [QTextStream](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qtextstream)
3. [Taking Commandline Arguments](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#taking-commandline-arguments)
4. [Making a basic QT class with signals and slots](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#making-a-basic-qt-class-with-signals-and-slots)
5. [Basic QT Dialog with Button, Label and MessageBox](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#basic-qt-dialog-with-button-label-and-messagebox)
5. [Resource File](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#resource-file)
5. [Creating Actions for Menu Bar, Tool Bar]()
6. [Basic QMainWindow with Central Widget, Menu Bar, Tool Bar](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#basic-qmainwindow-with-central-widget-menu-bar-tool-bar)
7. [QList, QStringList, QStringList::iterator, QListIterator](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qlist-qstringlist-qstringlistiterator-qlistiterator)
8. [QDir, QFileInfo, QDirIterator](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qdir-qfileinfo-qdiriterator)
9. [QFile](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qfile)
10. [QDate](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qdate)
11. [QThread](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#qthread)
12. [Serial Ports in QT](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#serial-ports-in-qt)
13. [Short GUI for Sending Characters to Arduino](https://github.com/rashfaqur/cheatsheets/blob/master/qt-cheatsheet.md#short-gui-for-sending-characters-to-arduino)

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

###### main.cpp ######
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

Project file.

###### simple.pro ######
```
TEMPLATE = app      # Type. Can be lib, subdir etc
TARGET = simple     # Executable name

QT += core

INCLUDEPATH += .
HEADERS =
SOURCES = main.cpp
```

#### Making a basic QT class with signals and slots ####

We will create our own string class based on QString. Our class name will be MyString. All QT classes inherits QObject class as base class. Q_OBJECT macro will be used for signals and slots. Slots are just regular member functions. They are called when a signal is emitted. signals are only function prototypes. Their arguments must match with the slots, they are emitted. Slots can be called as regular member function too. In the constructor QObject argument is taken as parent so that others can make QObject as parent for safe memory deallocation.

###### MyString.h ######
```c++
#ifndef MYSTRING_H
#define MYSTRING_H

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

#endif
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

    QObject::connect(a, SIGNAL(textChanged(const QString&)), b, SLOT(setText(const QString&)));

    a->setText(QString("a changed so, b will change too"));
    
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

#### Resource File ####
resource file is used to keep track of the resources used in the application. For resource file root is the project folder. Lets say we have kept new.png, cut.png and close.png int the images folder under project folder. We will add these to qt resource file. resource file's file extension is qrc.


###### resources.qrc ######
```xml
<!DOCTYPE RCC><RCC version="1.0">

<qresource>
	<file alias="new">images/new.png</file>
	<file alias="cut">images/cut.png</file>
	<file alias="close">images/close.png</file>
</qresource>

</RCC>
```

use: QIcon(":/images/new.png")

###### project.pro ######
```
RESOURCES += resources.qrc
```

#### Creating Actions for Menu Bar, Tool Bar ####

```c++
QAction *actionNew = new QAction(tr("&New"), this);
actionNew->setIcon(QIcon(":/images/new.png"));
actionNew->setShortcut(QKeySequence::New);
actionNew->setStatusTip(tr("Create New File"));
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

### QThread ###

Make a custom class inherited from QThread. Override `Thread::run()` method which will do the heavy works.
Each thread is started with `Thread::start()` method.

###### main.cpp ######
```c++
#include <QCoreApplication>
#include "mythread.h"

int main(int argc, char **argv){
    QCoreApplication app(argc, argv);

    MyThread th1("A"), th2("B"), th3("C");

    th1.start();
    th2.start();
    th3.start();

    return app.exec();
}
```

###### mythread.h ######
```c++
#ifndef MYTHREAD_H
#define MYTHREAD_H

#include <QThread>
#include <QString>

class MyThread: public QThread {

public:
    explicit MyThread(QString str);

    void run();

private:
    QString name;
};

#endif
```

###### mythread.cpp ######
```c++
#include "mythread.h"
#include <QDebug>

MyThread::MyThread(QString s)
    : name(s)
{
}

void MyThread::run(){
    for(int i = 0; i <= 100; i++){
        qDebug() << this->name << ":" << i;
    }
}
```

### Serial Ports in QT ###

#### QSerialPortInfo ####

`QList<QSerialPortInfo> QSerialPortInfo::availablePorts()` - availablePorst() static function returns a list of
available devices. Available devices are returned as QSerialPortInfo object 										</br>

Functions:

`QString portName()` - Return device port name. E.g ttyACM0, ttyUSB0 												</br>
`QString systemLocation()` - Returns port path / location. E.g /dev/ttyACM0 										</br>
`QString description` - Returns device description. 																</br>
`QString manufacturer` - Returns device manufacturer.																</br>
`QString serialNumber()` - Return device serial number.																</br>
`bool hasProductIdentifier()` - True if the device has valid product identifier number.								</br>
`quint16 productIdentifier()` - Returns product identifier number.													</br>
`bool hasVendorIdentifier()` - Returns true if the device has valid product number.									</br>
`quint16 vendorIdentifier()` - Returns vendor identifier number.													</br>
`bool isBusy()` - returns True if the serial port is busy.															</br>

### Short GUI for Sending Characters to Arduino ###

![ping arduino](http://i.imgur.com/8FnMVu8.png)

###### main.cpp ######
```c++
#include <QApplication>
#include "dialog.h"

int main(int argc, char *argv[]){
	QApplication app(argc, argv);

	Dialog dialog;
	dialog.show();

	return app.exec();
}
```

###### dialog.h ######
```c++
#ifndef DIALOG_H
#define DIALOG_H

#include <QDialog>
#include <QSerialPort>

class QLabel;
class QPushButton;
class QComboBox;
class QLineEdit;

class Dialog: public QDialog{
	Q_OBJECT

public:
	Dialog(QWidget *parent = 0);

public slots:
	void connect();
	void send();
	void handlePortError(const QString &error);
	void handleResponse();

signals:
	void portError(const QString &error);

private:
	QLabel *portLabel;
	QComboBox *portComboBox;
	QPushButton *connectButton;
	QLabel *dataLabel;
	QLineEdit *dataLineEdit;
	QPushButton *sendButton;
	QLabel *statusLabel;
	QLabel *status;
	QLabel *replyLabel;
	QLabel *reply;
	QSerialPort serialPort;
};

#endif
```

###### dialog.cpp ######
```c++
#include "dialog.h"
#include <QLabel>
#include <QPushButton>
#include <QComboBox>
#include <QLineEdit>
#include <QGridLayout>
#include <QSerialPortInfo>
#include <QByteArray>
#include <QDebug>

Dialog::Dialog(QWidget *parent)
	: QDialog(parent)
	, portLabel(new QLabel("Port:"))
	, portComboBox(new QComboBox())
	, connectButton(new QPushButton("Connect"))
	, dataLabel(new QLabel("Data:"))
	, dataLineEdit(new QLineEdit())
	, sendButton(new QPushButton("Send"))
	, statusLabel(new QLabel("Status:"))
	, status(new QLabel())
	, replyLabel(new QLabel("Reply:"))
	, reply(new QLabel())

{
	QList<QSerialPortInfo> infos = QSerialPortInfo::availablePorts();
	for(const QSerialPortInfo &info : infos){
		portComboBox->addItem(info.portName());
	}

	QGridLayout *mainLayout = new QGridLayout;
	mainLayout->addWidget(portLabel, 0, 0);
	mainLayout->addWidget(portComboBox, 0, 1);
	mainLayout->addWidget(connectButton, 0, 2);
	mainLayout->addWidget(dataLabel, 1, 0);	
	mainLayout->addWidget(dataLineEdit, 1, 1, 1, 2);
	mainLayout->addWidget(sendButton, 2, 1, 1, 1);
	mainLayout->addWidget(statusLabel, 3, 0);
	mainLayout->addWidget(status, 3, 1, 1, 2);
	mainLayout->addWidget(replyLabel, 4, 0);
	mainLayout->addWidget(reply, 4, 1, 1, 2);
	setLayout(mainLayout);

	QObject::connect(connectButton, SIGNAL(clicked()), this, SLOT(connect()));
	QObject::connect(sendButton, SIGNAL(clicked()), this, SLOT(send()));
	QObject::connect(this, SIGNAL(portError(const QString)), this, SLOT(handlePortError(const QString)));
	QObject::connect(&serialPort, SIGNAL(readyRead()), this, SLOT(handleResponse()));
}

void Dialog::connect(){
	if(serialPort.isOpen()){
		serialPort.close();
		connectButton->setText("Connect");
		return;
	}

	serialPort.setPortName(portComboBox->currentText());
	serialPort.setBaudRate(QSerialPort::Baud9600);

	if(!serialPort.open(QIODevice::ReadWrite)){
		emit portError(QString("Error: %1").arg(serialPort.errorString()));
		return;
	}

	status->setText(QString("Connected to %1.").arg(serialPort.portName()));

	connectButton->setText("Disconnect");
	return;
}

void Dialog::send(){
	QByteArray ba = dataLineEdit->text().toLocal8Bit();

	if(ba.isEmpty()){
		status->setText(QString("No data!"));
		return;
	}

	if(serialPort.isOpen() && serialPort.isWritable()){
		qint64 bytesWritten = serialPort.write(ba);
		serialPort.flush();

		if(bytesWritten == -1){
			emit portError(QString("Write failed! %1").arg(serialPort.errorString()));
			return;
		}
		else if(bytesWritten != ba.size()){
			emit portError(QString("Can't write all data! %1").arg(serialPort.errorString()));
			return;
		}
	
		status->setText(QString("%1 bytes written!").arg(bytesWritten));
	}

	return;
}

void Dialog::handlePortError(const QString &error){
	status->setText(error);	
}

void Dialog::handleResponse(){
	if(serialPort.isOpen() && serialPort.isReadable()){
		QByteArray readData = serialPort.readAll();
		while(serialPort.waitForReadyRead(5000)){
			readData += serialPort.readAll();
		}

		reply->setText(readData);
		return;
	}

	emit portError(QString("Port isn't open or not readable"));
}
```
