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
