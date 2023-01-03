//made by Prabhdeep Singh (22csu133)
#include<stdio.h>
#include<conio.h>
#include<math.h>
#include<string.h>
#include<stdlib.h>
#include<windows.h>
void account();
int main();
int transfermoney();
void login();
void intrest();
void gotoxy();
int loan();
int bankint();
void loginsu();
void display(char*);
void edit();
struct bank
{
    char name[50];
    char father[50];
    char mother[50];
    long long int aadhar;
    int age;
    long long int phone;
    char pass[6];
    char username[20];
    
};
void gotoxy(int x, int y)
{
    COORD c;
    c.X = x;
    c.Y =y;
    SetConsoleCursorPosition(GetStdHandle(STD_OUTPUT_HANDLE),c);
}

int main()
{
    int ch;
    gotoxy(30,8);
    printf("*# WELCOME TO DEEP BANK #*\n ");
    gotoxy(30,10);
    printf("click 1 for opening a new bank account\n ");
    gotoxy(30,12);
    printf("click 2 for getting information regarding your bank account\n");
    gotoxy(30,14);
    printf ("click 3 to login into  your account\n ") ;
    gotoxy(30,16);
    printf("click 4 for information about intrest rates of our bank\n");
    gotoxy(30,18);
    printf(" click 5 to edit your details");
    gotoxy(30,20);
    printf("enter a valid choice:  ");
    scanf("%d", &ch);
     switch (ch){
     case 1:{
        gotoxy(30,22);
         printf("  LETS START FILLING FORM FOR BANK ACCOUNT\n");
        account();
     }
        break;
     case 2:{
        gotoxy(30,22);
        printf(" you have selected for transactions:\n ");
        transfermoney();
     }
        break;
    case 3:{
        gotoxy(30,22);
        printf(" you have selected login option\n ");
        login();
    }
        break;
    case 4:{
        gotoxy(30,22);
        printf(" welcome to intrest calculator\n");
        intrest();
    }
        break;
    case 5:{
    	gotoxy(30,22);
    	printf(" edit your details\n");
    	edit();
    }
		break;
	
     default:{
        gotoxy(30,22);
        printf("error 404 enter a valid choice\n");
     }
        break;
     }
     return 0;
    
}
void account(void)
{
	system("cls");
    struct bank s;
    int i;
    char cha ;
    char x[6];
    FILE *fp; 
    fp = fopen("prabh.txt", "ab");
    gotoxy(30,10);
    printf("  LET'S START YOUR APPLICATION FOR OPENING A NEW BANK ACCOUNT\n   ");
    gotoxy(15,12);
    printf("  ENTER YOUR NAME:    ");
    scanf("%s", s.name);
    gotoxy(15,14);
    printf("  ENTER YOUR FATHER'S NAME:     ");
    scanf("%s", s.father);
    gotoxy(15,16);
    printf("  ENTER YOUR MOTHER'S NAME:     ");
    scanf("%s",s.mother);
    gotoxy(15,18);
    printf("  ENTER YOUR AADHAR NUMBER:     ");
    scanf("%lld",&s.aadhar);
    gotoxy(15,20);
    printf("  ENTER YOUR AGE AS PER AADHAR CARD:     ");
    scanf( "%d",&s.age);
    gotoxy(15,22);
    printf("  ENTER YOUR PHONE NUMBER:     ");
    scanf( "%lld",&s.phone);
    gotoxy(15,24);
    printf("   ENTER YOUR USERNAME:     ");
    scanf( "%s", s.username);
    gotoxy(15,26);
    printf("  SET A PASSWORD FOR YOUR E BANKING:     ");
    for (i=0;i<10;i++)
    {
        cha = getch();
        if (cha !=6){
            s.pass[i] = cha;
            cha = '*' ;
            printf("%c",cha);
            strcpy(x, s.pass);
        }
        else
        break;
    }fwrite(&s, sizeof(s),	1, fp);
    fclose(fp);
    gotoxy(30,30);
    printf("  \nACCOUNT SUCCESSFULLY CREATED\n    ");
    
    login();
    
        }

int transfermoney(void)
{
	system("cls");
    int character,add,send, total=10000,acc2;
    gotoxy(10,10);
    printf("click 1 to add money\n ");
    gotoxy(10,12);
    printf("  click 2 to transfer money\n");
    gotoxy(10,14);
    printf("enter a valid character\n");
    scanf("%d",&character);
    switch (character)
    {
    case 1:
        gotoxy(30,18);
        printf(" add money to acc:\n   ");
        gotoxy(30,20);
        printf("enter amount of money to be added:\n   ");
        scanf("%d",&add);
        gotoxy(30,22);
        printf("  %d rupeese is added to your account\n ", add);
        total= total+add;
        gotoxy(30,24);
        printf("current balance is rupees %d\n", total);
        break;
    case 2:
        gotoxy(30,18);
        printf(" transfer money to acc:\n    ");
        gotoxy(30,20);
        printf("enter amount of money to send:\n   ");
        scanf("%d",&send);
        gotoxy(30,22);
        printf(" enter bank acc number for sending money\n:     ");
        scanf("%d", &acc2);
        gotoxy(30,24);
        printf("  AMOUNT SUCCESSFULLY TRANSFERRED\n");
        total = total-send;
        gotoxy(30,26);
        printf("current balance is %d\n", total);
        break;
    default:
        break;
    }
    return total;
    main();
}
void login(void)
{
	system("cls");

	char username[50];
	char password[50];

	int i;
	char ch;
	FILE *fp;
	struct bank  s;

	fp = fopen("prabh.txt",	"rb");

	if (fp == NULL) {
		printf(" RECORD FILE CAN'T BE OPEN DUE TO SOME REASON...");
		exit(-1);
	}
	gotoxy(30, 2);
	printf(" ACCOUNT LOGIN ");
	gotoxy(5, 6);
	printf("\n\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\n");

	gotoxy(35, 10);
	printf(" tap to login.  \n");

	gotoxy(35, 12);
	printf(" ENTER YOUR USERNAME ");
	scanf("%s", &username);

	gotoxy(35, 14);
	printf(" ENTER YOUR PASSWORD..");

	for (i = 0; i < 50; i++) {
		ch = getch();
		if (ch != 13) {
			password[i] = ch;
			ch = '*';
			printf("%c", ch);
		}

		else
			break;
	}

	while (fread(&s, sizeof(s),
				1, fp)) {
		if (strcmp(username,
				s.username)
			== 0) {
		}
	}

	fclose(fp);
	loginsu();
    
}

void loginsu(void)
{
	int i,a;
	FILE* fp;
	char username[50];
	struct bank s;
	system("cls");
	printf("Fetching account details.....\n");
	for (i = 0; i < 200000000; i++) {
		i++;
		i--;
	}

	gotoxy(30, 10);
	printf("LOGIN SUCCESSFUL....");
	gotoxy(30, 20);
	printf("Press 1 to continue  \n");
    gotoxy(30,22);
    printf("  press 2 to logout ");
	scanf("%d", &a);
	switch (a)
	{
		case 1:{
			display(username);
			break;
		}
		case 2:{
			printf(" press enter to confirm for logout:\n   ");
			break;
		}
		default:
			break;
	}
	
	
}


void display(char username1[])
{
	system("cls");
	FILE* fp;
	fp = fopen("prabh.txt", "rb");
	struct bank s;

	if (fp == NULL) {
		printf("error in opening file");
	}

	while (fread(&s, sizeof(s),
				1, fp)) {
			gotoxy(30, 1);
			printf("WELCOME, %s", s.name);
			gotoxy(28, 2);
			printf("\n\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\n");
			gotoxy(40, 6);
			printf("YOUR ACCOUNT INFO ");
			gotoxy(40, 10);
			printf("NAME..%s\t", s.name);

			gotoxy(40, 12);
			printf("FATHER's NAME..%s\t",s.father);


			gotoxy(40, 14);
			printf("MOTHER's NAME..%s\t",s.mother);


			gotoxy(40, 16);
			printf("ADHAR CARD NUMBER..%lld\t",s.aadhar);


			gotoxy(40, 18);
			printf("MOBILE NUMBER..%lld\t",s.phone);


			gotoxy(40, 20);
			printf("AGE.. %d\t",s.age);

		}
	fclose(fp);

}

void intrest(void)
{
    system("cls");
    int ca;
    gotoxy(30,10);
    printf(" click 1 for loan intrest calculator:"); 
    gotoxy(30,12);
    printf("click 2 for intrest rates");
    gotoxy(30,14);
    printf("  enter a valid option:    ");
    scanf("%d", &ca);
    switch(ca){
        case 1:{
            gotoxy(30,18);
            printf(" THIS IS A SAMPLE FOR LOAN EMI AND INTREST");
            loan();
        }
            break;
        case 2:{
            gotoxy(30,18);
            printf(" BANK INTREST RATES ARE AT 3 PERCENT PER ANNUM ");
            bankint();
            
        }
        break;
        default:
        break;
    }
}
int loan(){
	system("cls");
	int loan, time, emi, loan1;

 gotoxy(15,20);
 printf("enter amount of loan:   ");
            scanf("%d", &loan);
            gotoxy(15,22);
            printf("intrest rates are 10 percent per annum:   ");
            gotoxy(15,24);
            printf(" enter time duration of repaying loan in years :   ");
            scanf("%d",&time);
            if (loan >= 100000)
            {
                loan1= loan +(loan)*0.1*time;
                emi = (loan1)/12*time;
                gotoxy(30,30);
                printf(" EMI per month is %d", emi);
            }
            else {
                gotoxy(30,30);
            	printf(" SORRY WE DONT PROVIDE LOAN LESS THEN 1 LAC RUPEES");
			}
            
            
            
}
int bankint(){
	system("cls");
	int balance, time, rate=3, amount;
    gotoxy(15,22);
    printf("enter amount of balance:\n   ");
            scanf("%d", &balance);
            gotoxy(15,24);
            printf(" enter time duration:\n");
            scanf("%d",&time);
            amount = balance +(balance)*0.03*time;
            gotoxy(30,28);
            printf(" total balance after %d years in your bank account will be %d", time, amount);
            
 }
            
void edit(){
	system("cls");
	FILE *fp ;
	fopen("prabh.txt", "r+");
	int a;
	long long int aadhar, aadhar1;
    int age, age1;
    long long int phone, phone1;
	char ch[50] , name[50], father[50], mother[50] ;
	char name1[50], father1[50], mother1[50];
    long long int ab;
	if (fp == NULL)
	{
		gotoxy(30,10);
		printf(" file cannot be open");
		exit(1);
	}
	while (1)
	{
		ch[50]= fgetc(fp);
		ab = fgetc(fp);
	//	if (ch == EOF)
	//	{
	//		printf("done");
		//	break;
		//}
		system("cls");
		gotoxy(30,10);
		printf(" 1 for name \n 2 for father name \n 3 for mother name \n 4 for aadhar number \n 5 for age \n 6 for phone number ");
		gotoxy(30,12);
		printf(" enter a choice");
		scanf(" %d", &a);
		system("cls");
		switch (a){
			case 1:{
				gotoxy(30,10);
				printf(" enter name you want to replace");
				scanf("%s", &name);
				gotoxy(30,12);
				printf(" enter name you want to replace with");
				scanf("%s", &name1);
				if (ch == name)
				{
					fputc( name1[50], fp);
				}
				break;
			}
				case 2:{
				gotoxy(30,10);
				printf(" enter name you want to replace");
				scanf("%s", &father);
				gotoxy(30,12);
				printf(" enter name you want to replace with");
				scanf("%s", &father1);
				if (ch == father)
				{
					fputc( father1[50], fp);
				}
				break;
	     	}
	     		case 3:{
	     		gotoxy(30,10);
				printf(" enter name you want to replace");
				scanf("%s", &mother);
				gotoxy(30,12);
				printf(" enter name you want to replace with");
				scanf("%s", &mother1);
				if (ch == mother)
				{
					fputc( mother1[50], fp);
				}
				break;
			}
			case 4:{
				gotoxy(30,10);
				printf(" enter aadhar you want to replace");
				scanf("%s", &aadhar);
				gotoxy(30,12);
				printf(" enter aadhar you want to replace with");
				scanf("%s", &aadhar1);
				if (ab == aadhar)
				{
					fputc( aadhar1, fp);
				}
				break;
			}
			case 5:{
				gotoxy(30,10);
				printf(" enter age you want to replace");
				scanf("%s", &age);
				gotoxy(30,12);
				printf(" enter age you want to replace with");
				scanf("%s", &age1);
				if (ab == age)
				{
					fputc( age1, fp);
				}
				break;
			}
			case 6:{
			    gotoxy(30,10);
				printf(" enter phone number you want to replace");
				scanf("%s", &phone);
				gotoxy(30,12);
				printf(" enter phone number you want to replace with");
				scanf("%s", &phone1);
				if (ab == phone)
				{
					fputc( phone1, fp);
				}
				break;
			}
			
		}
	}
	fclose(fp);
}
