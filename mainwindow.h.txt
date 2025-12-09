#ifndef MAINWINDOW_H
#define MAINWINDOW_H
#include "student.h"
#include <QVector>
#include<QList>
#include <QMainWindow>
#include <QTableWidgetItem>

QT_BEGIN_NAMESPACE
namespace Ui {
class MainWindow;
}
QT_END_NAMESPACE

class MainWindow : public QMainWindow
{
    Q_OBJECT

public:
    MainWindow(QWidget *parent = nullptr);
    ~MainWindow();

private slots:
    void on_pushButton_clicked();
    void on_displayButton_clicked();
    void on_deleteButton_clicked();
    void on_updateButton_clicked();
    void on_pushButton_2_clicked();
    void on_tableWidget_itemClicked(QTableWidgetItem *item);

private:
    Ui::MainWindow *ui;
    QList<Student> records;
};
#endif // MAINWINDOW_H
