# SchoolManagement
Advice career guidelines to students and parents based on student  performance in academics ,sports and other activities


#include <iostream>

#include <stdio.h>

#include <cstring>

#include <stdlib.h>

using namespace std;

class student

{public:

	int rollno;

	char name[10];

	char fname[10];

	long int cell;

	char address[20];

	int date;

	int month;

	int year;

	float acadper;

	float sportper;

	int pref;

};

class fclass

{

	int total;

	student rec[50];

public:

	void schoolmanagement();

	void show_data(int searchkey);

	void get_data(int i);

void search_student(int searchkey);

void add_student(int j);

void edit_student(int idnumber);

 void getfromfile();

};

int main()

{

	fclass we;

	we.getfromfile();

	we.schoolmanagement();

	return 0;

}

void fclass::schoolmanagement()

{

	int choice,lol;

	int idnumber;

	int searchkey;

	while (1)

	{

		cout << "\n\t\tWHAT DO YOU WANT TO DO ? " << endl;

		cout << "\t\t----------------------" << endl;

		cout << "\t\t1::ADD STUDENT" << endl;

		cout << "\t\t2-EDIT STUDENT" << endl;

		cout << "\t\t3-SEARCH STUDENT" << endl;

		cout << "\t\t4-QUIT PROGRAM" << endl;

		cout << "\t\t----------------------" << endl;

		cout << "ENTER YOUR CHOICE : ";


		cin >> choice;

		switch (choice)

		{

		case 1:

			cout<<"ENTER STUDENT ID\n";

			cin>>lol;

			add_student(lol);

			break;

		case 2:

			if (rec[0].rollno == 0)

			{

				cout << "PLEASE ADD STUDENTS FIRST." << endl;

				schoolmanagement();

			}

			else

			{

				cout << endl;

				cout << "------------------------------------------------------------------------------------" << endl;

				cout << "---------------------------STUDENT RECORD TABLE-------------------------------------" << endl;

				cout << "------------------------------------------------------------------------------------" << endl;

				cout << "ID   "

					 << "ROLL   "

					 << "NAME      "

					 << "FATHER\tCELL NO.      "

					 << "DOB          "

					 << "ADDRESS";

				cout << "ACADEMIC PERCENTAGE\tSPORTS PERCENTAGE\tPREFERENCE\n\n";

				cout << "------------------------------------------------------------------------------------" << endl;


				for (int i = 0; i <total ; i++)

				{

					show_data(i);

				}


				cout << "------------------------------------------------------------------------------------" << endl;

				cout << "WHICH ID NUMBER YOU WANT TO EDIT : ";

				cin >> idnumber;


				if (idnumber >total || idnumber < 0)

				{

					cout << "\nINVALID ID NUMBER." << endl;

				}

				else

				{

					edit_student(idnumber);

				}

			}

			break;


		case 3:

			if (rec[0].rollno == 0)

			{

				cout << "PLEASE ADD STUDENTS FIRST." << endl;

				schoolmanagement();

			}

			else

			{

				cout << "ENTER ROLL NUMBER OF STUDENT YOU WANT TO SEARCH :: ";

				cin >> searchkey;

				search_student(searchkey);

			}

			break;

		case 4:

			exit(0);

		default:

			cout << "INVALID CHOICE." << endl;

			schoolmanagement();

		}

	}

}


void fclass::get_data(int i)

{

	cout << "ENTER ROLL NUMBER IN THIS FORMAT (1XXX):: ";

	cin >> rec[i].rollno;

	while (rec[i].rollno <= 999 || rec[i].rollno > 2000)

	{

		cout << "ENTER CORRECT ROLL NUMBER\n";

		cin >> rec[i].rollno;

	}

	cout << "ENTER STUDENT NAME :: ";

	cin >> rec[i].name;


	cout << "ENTER STUDENT'S FATHER NAME :: ";

	cin >> rec[i].fname;


	cout << "PHONE NUMBER SHOULD CONTAIN EXACTLY 10 DIGITS\n";

	cin >> rec[i].cell;


	cout << "ENTER STUDENT DOB (dd/mm/yyyy):: \n";

	cin >> rec[i].date >> rec[i].month >> rec[i].year;

	while (rec[i].year > 2019)

	{

		cout << "ENTER CORRECT YEAR\n";

		cin >> rec[i].year;

	}


	while (rec[i].month < 0 || rec[i].month > 12)

	{

		cout << "ENTER CORRECT MONTH \n";

		cin >> rec[i].month;

	}


	if (rec[i].month == 1 || rec[i].month == 3 || rec[i].month == 5 || rec[i].month == 7 || rec[i].month == 8 || rec[i].month == 10 || rec[i].month == 12)

	{

		if (rec[i].date < 32)

			cout << rec[i].date << "-" << rec[i].month << "-" << rec[i].year << endl;

		else

			cout << "DATE IS WRONG\n";

	}

	else if (rec[i].month == 2)

	{

		if (rec[i].year % 4 == 0)

		{

			if (rec[i].date < 30)

			{

				cout << "IT IS A LEAP YEAR\n";

				cout << rec[i].date << "-" << rec[i].month << "-" << rec[i].year << endl;

			}

			else

				cout << "DATE IS WRONG";

		}

		else

		{

			if (rec[i].date < 29)

				cout << rec[i].date << "-" << rec[i].month << "-" << rec[i].year << endl;

			else

				cout << "DATE IS WRONG\n";

		}

	}

	else

	{

		if (rec[i].date < 31)

			cout << rec[i].date << "-" << rec[i].month << "-" << rec[i].year << endl;

		else

			cout << "DATE IS WRONG\n";

	}

	cout << "ENTER STUDENT'S ADDRESS :: ";

	cin >> rec[i].address;

	cout << "ENTER STUDENT ACADEMIC PERCENTAGE :: ";

	cin >> rec[i].acadper;

	cout << "ENTER STUDENT ACADEMIC PERCENTAGE :: ";

	cin >> rec[i].sportper;

	if (rec[i].acadper > rec[i].sportper)

		rec[i].pref = 1;

	else

		rec[i].pref = 0;

	FILE *fp;

	fp = fopen("b.txt", "a+");

	rewind(fp);

	fseek(fp,80*i,SEEK_SET);

	cout << "fooo" << i << endl;


	fprintf(fp, "%d", rec[i].rollno);

fprintf(fp,"\n");

	fprintf(fp, "%ld", rec[i].cell);

	fprintf(fp,"\n");


	fprintf(fp, "%d", rec[i].date);

	fprintf(fp,"\n");

	fprintf(fp, "%d", rec[i].month);

fprintf(fp,"\n");


	fprintf(fp, "%d", rec[i].year);

fprintf(fp,"\n");


		fprintf(fp, "%s", rec[i].name);

fprintf(fp,"\n");


	fprintf(fp, "%s", rec[i].fname);

fprintf(fp,"\n");


	fprintf(fp, "%s", rec[i].address);

	fprintf(fp,"\n");

	fprintf(fp,"%f",rec[i].acadper);

	fprintf(fp,"\n");

		fprintf(fp,"%f",rec[i].sportper);

		fprintf(fp,"\n");

	fclose(fp);

}

void fclass::show_data(int searchkey)

{

	int a, n = 0;

	int i = searchkey;

	cout << i << "    ";

	cout << rec[i].rollno << "   ";

	n = strlen(rec[i].name);

	cout << rec[i].name;

	for (a = 0; a != (12 - n); a++)

		cout << " ";

	n = strlen(rec[i].fname);

	cout << rec[i].fname;


	for (a = 0; a != (13 - n); a++)

		cout << " ";


	cout << rec[i].cell << "   ";

	cout << rec[i].date << "-" << rec[i].month << "-" << rec[i].year << "  ";

	cout << rec[i].address;

	cout << rec[i].acadper << "\t" << rec[i].sportper;


	if (rec[i].pref == 1)

		cout << "ACADEMICS\n\n";

	else

		cout << "SPORTS IS BEST\n\n";

}


void fclass::search_student(int searchkey)

{

	for (int i = 0; i < 50; i++)

	{

		if (rec[i].rollno == searchkey)

		{

			cout << "ID   "

				 << "ROLL   "

				 << "NAME        "

				 << "FATHER       CELL NO.     "

				 << "DOB         "

				 << "ADDRESS\t"

				 <<"ACADEMIC PERCENTAGE\tSPORTS PERCENTAGE\tPREFERENCE\n\n";

			show_data(i);

		}

	}

}


void fclass::add_student(int j)

{

	total++;

	get_data(j);

	cout << endl;

	cout << "-----------------------------------------------------------------------------------------------" << endl;

	cout << "------------------------------------STUDENT RECORD TABLE---------------------------------------" << endl;

	cout << "-----------------------------------------------------------------------------------------------" << endl;

	cout << "ID   "

		 << "ROLL   "

		 << "NAME        "

		 << "FATHER       CELL NO.     "

		 << "DOB         "

		 << "ADDRESS\tACADEMIC PERCENTAGE\tSPORTS PERCENTAGE\tPREFERENCE\n\n";

	cout << "-----------------------------------------------------------------------------------------------" << endl;


	for (int i = 0; i < j+1; i++)

	{

		show_data(i);

	}

	cout << "-----------------------------------------------------------------------------------------------" << endl;

	cout << "------------------------------------FINISH-----------------------------------------------------" << endl;

	cout << "-----------------------------------------------------------------------------------------------" << endl;


	schoolmanagement();

}


void fclass::edit_student(int idnumber)

{

	for (int i = 0; i < total; i++)

	{

		if (idnumber == i)

		{

			cout << "\nEXISTED INFORMATION ABOUT THIS RECORD.\n\n";

			cout << "------------------------------------------------------------------------------------" << endl;

			cout << "ID   "

				 << "ROLL   "

				 << "NAME      "

				 << "FATHER\tCELL NO.      "

				 << "DOB          "

				 << "ADDRESS\t";

			cout << "ACADEMIC PERCENTAGE\tSPORTS PERCENTAGE\tPREFERENCE\n\n";

			cout << "------------------------------------------------------------------------------------" << endl;

			show_data(i);

			cout << "\n\nEnter NEW DATA OF STUDENT.\n\n";

			get_data(i);

			cout << "\n\nRECORD UPDATED SUCCESSFULLY." << endl;

			schoolmanagement();

		}

	}

}


void fclass::getfromfile()

{

	FILE *fp = fopen("b.txt", "r");

	if (fp == NULL)

		_exit(0);

	int i=0;

	rewind(fp);

	while(!feof(fp))

	{

	total++;	

	fscanf(fp, "%d", &rec[i].rollno);

	fscanf(fp, "%ld", &rec[i].cell);

	fscanf(fp, "%d", &rec[i].date);

	fscanf(fp, "%d", &rec[i].month);

	fscanf(fp, "%d", &rec[i].year);

	fscanf(fp, "%s", &rec[i].name);

	fscanf(fp, "%s", &rec[i].fname);

	fscanf(fp, "%s", &rec[i].address);

    fscanf(fp, "%f", &rec[i].acadper);

	fscanf(fp, "%f", &rec[i].sportper);

	cout<< rec[i].rollno << endl;

	cout << rec[i].name << endl;

	cout << rec[i].fname << endl;

	cout << rec[i].date << endl;

	cout << rec[i].year << endl;

	cout << rec[i].sportper << endl;

	i++;

	}

	fclose(fp);

}


