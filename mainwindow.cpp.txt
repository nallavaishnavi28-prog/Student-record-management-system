#include "mainwindow.h"
#include "ui_mainwindow.h"
#include <QMessageBox>
#include<QString>
#include<QDebug>

MainWindow::MainWindow(QWidget *parent)
    : QMainWindow(parent)
    , ui(new Ui::MainWindow)
{
    ui->setupUi(this);
    ui->tableWidget->setColumnCount(5);
    ui->tableWidget->setHorizontalHeaderLabels({"Name", "Subject", "Roll",
                "Semester", "Grade"});
}

MainWindow::~MainWindow()
{
    delete ui;
}

void MainWindow::on_pushButton_clicked()
{
    Student s;
    s.name = ui->nameLineEdit->text();
    s.subject = ui->subjectLineEdit->text();
    s.roll = ui->rollLineEdit->text().toInt();
    s.semester = ui->semesterLineEdit->text().toInt();
    s.grade = ui->gradeLineEdit->text();

   records.append(s);
    QMessageBox::information(this, "Success", "Student added Successfully");
    qDebug()<<"saved: "<< s.name<<" "<<s.subject<<" "<<s.roll<<" "
            <<s.semester<<" "<<s.grade;
    ui->nameLineEdit->clear();
    ui->subjectLineEdit->clear();
    ui->rollLineEdit->clear();
    ui->semesterLineEdit->clear();
    ui->gradeLineEdit->clear();
}

void MainWindow::on_displayButton_clicked()
{
    ui->tableWidget->setRowCount(records.size());

    for (int i = 0; i < records.size(); i++)
    {
        ui->tableWidget->setItem(i, 0, new QTableWidgetItem(records[i].name));
        ui->tableWidget->setItem(i, 1, new QTableWidgetItem(records[i].subject));
        ui->tableWidget->setItem(i, 2, new QTableWidgetItem(QString::number(records[i].roll)));
        ui->tableWidget->setItem(i, 3, new QTableWidgetItem(QString::number(records[i].semester)));
        ui->tableWidget->setItem(i, 4, new QTableWidgetItem(records[i].grade));
    }
}

void MainWindow::on_deleteButton_clicked()
{
    int row = ui->tableWidget->currentRow();
    if (row >= 0)
    {
        records.removeAt(row);
        ui->tableWidget->removeRow(row);
    }
     QMessageBox::information(this, "Success", "Student deleted Successfully");
}
void MainWindow::on_updateButton_clicked()
{
    int row = ui->tableWidget->currentRow();

    if (row >= 0)
    {
        records[row].name = ui->nameLineEdit->text();
        records[row].subject = ui->subjectLineEdit->text();
        records[row].roll = ui->rollLineEdit->text().toInt();
        records[row].semester = ui->semesterLineEdit->text().toInt();
        records[row].grade = ui->gradeLineEdit->text();

        qDebug() << "UPDATED ROW:" << row;
        qDebug() << records[row].name
                 << records[row].subject
                 << records[row].roll
                 << records[row].semester
                 << records[row].grade;
        on_displayButton_clicked();   // refresh table
        QMessageBox::information(this,"done", "Updated successfully!");
    }
}
void MainWindow::on_tableWidget_itemClicked(QTableWidgetItem *item)
{
    int row = item->row();

    ui->nameLineEdit->setText(ui->tableWidget->item(row, 0)->text());
    ui->subjectLineEdit->setText(ui->tableWidget->item(row, 1)->text());
    ui->rollLineEdit->setText(ui->tableWidget->item(row, 2)->text());
    ui->semesterLineEdit->setText(ui->tableWidget->item(row, 3)->text());
    ui->gradeLineEdit->setText(ui->tableWidget->item(row, 4)->text());

}
    void MainWindow::on_pushButton_2_clicked()
    {
      close();
    }




