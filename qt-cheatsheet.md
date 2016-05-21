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
QStringStream
QFile
QList
QStringList
QStringList::iterator
QListIterator<QString>
QDirIterator
