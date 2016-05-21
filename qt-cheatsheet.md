### QT Cheatsheet ###

#### QString ####

```c++
QString hello = "Hello, World";
qDebug() << hello << "\n";
```
```c++
int number = 10;
QString string = "This a cute string";
QString show = QString("My number is: %1 and my string is: %2\n").arg(number).arg(string);
qDebug() << show;
```

#### QStringStream ####

```c++
QString qstr;
QStringStream cout(stdout);				/* stream text to stdout */
QStringStream cin(stdin);				/* take input from stdin */
QStringStream toStringObject(&qstr);	/* store in a Qstring */

cout << "Hello, world!\n"
cout << QString("First prime number is: %1\n").arg(2);

QString inputString;
cin >> inputString;
cout << inputSting;

toStringObject << "This is a literal string\n" << QString("A QString with number %1\n").arg(10) << inputString << "\n";
cout << qstr;
```

#### QFile ####

```c++
QFile file("myTextFile.txt");
file.open(QIODevice::WriteOnly);

QStringStream outFile(&file);
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

QDialog
QInputDialog
QFileDialog
QMessageBox
