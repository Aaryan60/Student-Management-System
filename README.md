# Student-Management-System
In this project you will able to find how a code is written for creating student management system.


   #include<iostream.h>
   #include<conio.h>
   #include<dos.h>
   #include<stdio.h>
   #include<string.h>
   #include<process.h>
   #include<fstream.h>

      void START();

     class Student
     {
	 char id[30];
	 char name[100];
	 char branch[10];
	 char mobile[50];
	 double marks;

	 public:
	    Student()
	    {
		strcpy(id  , NULL);
		strcpy(name  , NULL);
		strcpy(branch , NULL);
		strcpy(mobile , NULL);
		marks = 0;
	    }

	    void getdata();
	    void display();

	    char* get()
	    {
		return id;
	    }
     }S;

	  void Student :: getdata()
	  {
		 clrscr();
	       textcolor(WHITE);

		gotoxy(10 , 3);
	       cprintf("ENTER STUDNET ID : ");

		gotoxy(10 , 5);
	       cprintf("ENTER NAME    : ");

		gotoxy(10 , 7);
	       cprintf("ENTER BRANCH  : ");

		gotoxy(10 , 9);
	       cprintf("ENTER MOBILE  : ");

	       gotoxy(10 , 11);
	       cprintf("TOTAL MARKS   : ");


	       do
	       {
		     gotoxy(29 , 3);
		     cprintf("     ");
		     gotoxy(29 , 3);
		     gets(id);

	       }while(id <= 0);

	       do
	       {
		     gotoxy(26 , 5);
		     cprintf("            ");
		     gotoxy(26 , 5);
		     gets(name);

	       }while(strcmp(name , NULL) == 0);

	       do
	       {
		     gotoxy(26 , 7);
		     cprintf("            ");
		     gotoxy(26 , 7);
		     gets(branch);

	       }while(strcmp(branch , NULL) == 0);

	       do
	       {
		     gotoxy(26 , 9);
		     cprintf("            ");
		     gotoxy(26 , 9);
		     gets(mobile);

	       }while(strcmp(mobile , NULL) == 0);

	       do
	       {
		     gotoxy(26 , 11);
		     cprintf("            ");
		     gotoxy(26 , 11);
		     cin>>marks;

	       }while(marks < 0);
	  }

	  void Student::display()
	  {
		 clrscr();
	       textcolor(WHITE);

		gotoxy(10 , 3);
	       cprintf(" STUDENT ID   : %s ", id);

		gotoxy(10 , 5);
	       cprintf(" STUDENT NAME : %s ",name);

		gotoxy(10 , 7);
	       cprintf(" BRANCH       : %s ", branch);

		gotoxy(10 , 9);
	       cprintf(" MOBILE       : %s ", mobile);

	       gotoxy(10 , 11);
	       cprintf(" TOTAL MARKS  : %lf ",marks);
	  }

   void ADD()
   {
	int choice;

	fstream obj("student.txt", ios::out);

	   do
	   {
		   fflush(stdin);
		    S.getdata();

		  obj.write((char *) &S, sizeof(S));

		     fflush(stdin);
		     gotoxy(20 , 15);
		     cprintf(" DO YOU WANT TO ADD MORE RECORDS (1/0) : ");
			cin>>choice;

		    if(choice != 1)
		    {
			  break;
		    }

	   }while(choice == 1);

	      obj.close();

		   gotoxy(10 , 17);
	      cprintf(" RECORDS ADDED SUCCESSFULLY! ");
   }

   void MODIFY()
   {
	  int flag=1;
	  char id[30];

	     gotoxy(12 , 17);
	  cprintf("\n Enter student id to be modified : ");
	      gets(id);

	fstream obj1("student.txt", ios::in);
	fstream obj2("temp.txt",ios::out);

	    while(!obj1.eof() && obj1.read((char *) &S, sizeof(S)))
	    {
		 if(strcmpi(S.get(), id) == 0)
		 {
		      flag = 2;
		      S.getdata();
		 }

		 obj2.write((char *) &S, sizeof(S));
	    }

		 obj1.close();
		 obj2.close();

	    if(flag == 1)
	    {
		   gotoxy(15 , 21);
		 cprintf(" RECORD NOT FOUND ");
	    }
	    else
	    {
		   gotoxy(15 , 21);
		 cprintf(" RECORD MODIFIED SUCCESSFULLY!");
	    }

		 remove("student.txt");
		 rename("temp.txt", "student.txt");
   }

   void DELETE()
   {
	  int flag=1;
	  char id[30];

	     gotoxy(12 , 17);
	  cprintf("\n Enter student id to be deleted : ");
	      gets(id);

	fstream obj1("student.txt", ios::in);
	fstream obj2("temp.txt",ios::out);

	    while(!obj1.eof() && obj1.read((char *) &S, sizeof(S)))
	    {
		 if(strcmpi(S.get(), id) == 0)
		 {
		      flag = 2;
		 }
		 else
		 {
		    obj2.write((char *) &S, sizeof(S));
		 }
	    }

		 obj1.close();
		 obj2.close();

	    if(flag == 1)
	    {
		   gotoxy(15 , 20);
		 cprintf(" RECORD NOT FOUND ");
	    }
	    else
	    {
		   gotoxy(15 , 21);
		 cprintf(" RECORD DELETED SUCCESSFULLY! ");
	    }

		 remove("student.txt");
		 rename("temp.txt", "student.txt");

   }

   void DISPLAY()
   {
	fstream obj("student.txt", ios::in);

	     while(!obj.eof() && obj.read((char *) &S, sizeof(S)))
	     {
		  S.display();
		  getch();
	     }

		obj.close();
		gotoxy(12, 18);
		cprintf("NO RECORD FOUND");
   }

   void WELCOME()
   {
       char *s ="WELCOME TO";
       char *s2="MY C++ PROJECT";
	    int i;

	  textcolor(2);

       for(i=0 ; i<10 ; i++)
       {
	       delay(70);
	    gotoxy(33+i,10);
	    cprintf("%c",*s);
	      s++;
       }

       for(i=0 ; i<14 ; i++)
       {
	       delay(70);
	    gotoxy(32+i, 12);
	    cprintf("%c",*s2);
	      s2++;
       }

	   textcolor(WHITE);
	   gotoxy(55 , 19);
	 cprintf(" PROJECT MADE BY : ");

	   textcolor(WHITE);
	   gotoxy(58 , 21);
	  cprintf("  AARYAN RAUT ");
	   gotoxy(58 , 22);
	  cprintf("  VIVEK MASKE ");
	   gotoxy(58 , 23);
	  cprintf("  ADITYA KADAM ");
	   gotoxy(58 , 24);
	  cprintf("  ROHAN MADHAVI ");

	     getch();
   }

   void PASSWORD()
   {
	 char user[50],pass[50];

	   clrscr();

	    textcolor(WHITE);
	      gotoxy(30,8);
	   cprintf("USERNAME :");
	      gotoxy(30,10);
	   cprintf("PASSWORD :");

	    gotoxy(41,8);
	    cprintf("                  ");
	    gotoxy(41,10);
	    cprintf("                  ");

	do
	{
	    gotoxy(41,8);
	    gets(user);
	}while( strcmp(user,NULL)==0);

	do
	{
	     gotoxy(41,10);
	     gets(pass);
	}while(strcmp(pass,NULL)==0);


	     if(strcmpi(pass,"ADMIN")!=0 || strcmpi(user,"ADMIN")!=0)
	     {
			textcolor(RED + BLINK);
			gotoxy(27 , 15);
			cprintf("INVALID USERNAME OR PASSWORD");
			getch();
			textcolor(WHITE);
			PASSWORD();
	     }
	     else
	     {
			textcolor(YELLOW);
			gotoxy(27 , 15);
			cprintf("LOGIN SUCCESSFUL");
			textcolor(WHITE);
	     }
   }

   void STUDENT()
   {
	  int flag=1;
	  char id[30];

	     gotoxy(12 , 17);
	  cprintf("\n Enter student id : ");
	      gets(id);

	fstream obj1("student.txt", ios::in);

	    while(!obj1.eof() && obj1.read((char *) &S, sizeof(S)))
	    {
		 if(strcmpi(S.get(), id) == 0)
		 {
		      flag = 2;
		      S.display();
		      break;
		 }
	    }

		 obj1.close();

	    if(flag == 1)
	    {
		   gotoxy(15 , 21);
		 cprintf(" RECORD NOT FOUND ");
	    }
   }

   int menu2()
   {
	int choice;

	 clrscr();

	   textcolor(WHITE);
	    gotoxy(10 , 3);
	 cprintf("1] ADD NEW RECORD ");
	   gotoxy(10 , 5);
	 cprintf("2] MODIFY RECORD ");
	   gotoxy(10 , 7);
	 cprintf("3] DELETE A RECORD ");
	   gotoxy(10 , 9);
	 cprintf("4] DISPLAY RECORDS ");
	   gotoxy(10 , 11);
	 cprintf("5] GO BACK TO MAIN MENU ");

	   gotoxy(10 , 13);
	 cprintf("ENTER YOUR CHOICE : ");
	     cin>>choice;

	     return choice;
   }

   void ADMIN()
   {
       int ch;

	 do
	 {
	     ch = menu2();

	     switch(ch)
	     {
		  case 1:
			   ADD();
			   break;
		  case 2:
			   MODIFY();
			   break;
		  case 3:
			   DELETE();
			   break;
		  case 4:
			   DISPLAY();
			   break;
		  case 5:
			   START();
			   break;
		  default:
			   cprintf("\n\n INVALID INPUT ");
	     }
		 getch();
	 }while(ch != 5);
   }

   int menu()
   {
	 int choice;

	 clrscr();

	   textcolor(WHITE);
	    gotoxy(10 , 3);
	 cprintf("1] ADMIN ");
	   gotoxy(10 , 5);
	 cprintf("2] STUDENT ");
	   gotoxy(10 , 7);
	 cprintf("3] EXIT ");

	   gotoxy(10 , 9);
	 cprintf("ENTER YOUR CHOICE : ");
	     cin>>choice;

	     return choice;
   }

   void START()
   {
       int choice;

	clrscr();

	do
	{
	     choice = menu();

	       switch(choice)
	       {
		    case 1:
			     PASSWORD();
			     ADMIN();
			     break;
		    case 2:
			     STUDENT();
			     break;
		    case 3:
			      gotoxy(20, 11);
			      cprintf("THANKS");
			      getch();
			      exit(0);
		    default:
			     cprintf("PLEASE ENTER VALID CHOICE...");
	       }
		 getch();
	}while(choice != 3);
   }

   void main()
   {
       clrscr();

       WELCOME();
       START();

       getch();
   }

