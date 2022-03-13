#include <stdio.h>
#include <stdlib.h>
#include <string.h>
/*
name
gender
block
room number
registration number
people sharing
rank list
remaining blocks/rooms


struct room
{
    char name[50];
    char reg_no[10];
    char block_name;
    int room_no[4];
    struct room *next;
}*head,*rear;

*/

struct list
{
	char name[30];
    char reg_no[10];
    float CGPA;
    char gender;
    struct list *next;
}*front=NULL,*rear=NULL,*nw,*head=NULL,*tail=NULL;

//---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

void block_name()
{
    char b[5];
    printf("\nEnter which block you want: ");
    scanf("%s",&b);
    printf("\nThe block alloted to you is:- %s\n",b);
    return b;
}

//--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

int room_number()
{
    int max,min,n,sharing,type ;
    printf("\nThe following are the options for your hostel:- \n\t(1) A.C. room\n\t(2) Non - A.C. room\n ");
    scanf("%d",&type);
    if (type<3)
    {

    printf("\nEnter the number of sharing you want: \n\t(1) 1 bedded sharing\n\t(2) 2 bedded sharing\n\t(3) 3 bedded sharing\n\t(4) 6 bedded sharing\n ");
    scanf("%d",&sharing);
    if (sharing <5)
    {

    if (sharing==1)
    {
            max=1143;
            min=1005;
            n=(rand()%(max-min+1))+min;
    }
    if(sharing==2)
    {
        max=900;
        min=700;
        n=(rand()%(max-min+1))+min;
    }
    if  (sharing==3)
    {
        max=320;
        min=112;
        n=(rand()%(max-min+1))+min;
    }
    if (sharing==4)
    {
        max=650;
        min=431;
        n=(rand()%(max-min+1))+min;
    }

    }
    else
    {
        printf("It is not an option. RETRY!!\n");
        room_number();
    }

    printf("\nThe room alloted to you is:- %d\n",n);

    }
    else
    {
        printf("It is not an option. RETRY!!\n");
        room_number();
    }

    return n;
}

//--------------------------------------------------------------------------------------------------------------------------------------------------------------------

void display()
{
    struct list *temp=front;

    printf("\n\t\t ~~RANK LIST FOR MEN'S HOSTEL ALLOTMENT~~\n\n");
    while (temp->next!=NULL)
    {
        //if (temp->gender=='M' || temp->gender=='m')
            printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp->name,temp->reg_no,temp->CGPA);
        temp=temp->next;

    }
    //if (temp->gender=='M' || temp->gender=='m')
        printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp->name,temp->reg_no,temp->CGPA);

    printf("\n\t\t ~~RANK LIST FOR WOMEN'S HOSTEL ALLOTMENT~~\n\n");
    temp=head;

    while (temp->next!=NULL)
    {
      //  if (temp->gender=='F' || temp->gender=='f')
            printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp->name,temp->reg_no,temp->CGPA);
        temp=temp->next;
    }
    //if (temp->gender=='F' || temp->gender=='f')
    printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp->name,temp->reg_no,temp->CGPA);
}

//---------------------------------------------------------------------------------------------------------------------------------------------

void enqueue()
{
    nw= (struct list*)malloc(sizeof(struct list));
    printf("\nEnter your Name: ");
    //scanf("%[^\n]%*c",&nam);
    scanf("%s",&nw->name);
    printf("\nEnter you Registration number: ");
    scanf("%s",&nw->reg_no);
    printf("\nEnter your CGPA: ");
    scanf("%f",&nw->CGPA);
    printf("\nEnter your gender [Put 'M' for Male and 'F' for Female]: ");
    scanf("%s",&nw->gender);


    if (nw->gender=='M' || nw->gender=='m')
    {
    if (front==NULL)
    {

    	nw->next=NULL;
        front=nw;
        rear=nw;
    }
    else
    {

    	rear->next=nw;
        rear=nw;
        rear->next=NULL;
    }
}


if(nw->gender=='F' || nw->gender=='f' )
{
if (head==NULL)
    {

    	nw->next=NULL;
        head=nw;
        tail=nw;
    }
    else
    {

    	tail->next=nw;
        tail=nw;
        tail->next=NULL;
    }
}
}

//------------------------------------------------------------------------------------------------------------------------------------------------------------------

void details()
{
    int k,f;

    while(f=1)
    {
        printf("\nEnter what you want to do:\n\t(1) Enter student details\n\t(2) Exit\n");
        scanf("%d",&k);

    switch(k)
    {
    case 1:
        enqueue();
        break;

    case 2:
       return;
    }
    }
}

//-----------------------------------------------------------------------------------------------------------------------------------------------------

/* Bubble sort the given linked list */
void bubbleSort()
{
    int swapped, i;
    struct list *ptr1;
    struct list *lptr = NULL;
    struct list *ptr2;
    struct list *lptr2=NULL;

//SORTING MENS LIST
    /* Checking for empty list */
    if (front == NULL)
        return;

    else if (front->next==NULL)
        return;

    do
    {
        swapped = 0;
        ptr1 = front;

        while (ptr1->next != lptr)
        {
            if (ptr1->CGPA < ptr1->next->CGPA)
            {
                swap(ptr1, ptr1->next);
                swapped = 1;
            }
            ptr1 = ptr1->next;
        }
        lptr = ptr1;
    }
    while (swapped);


// SORTING WOMEN LIST

 if (head == NULL)
       return;

 else if (head->next==NULL)
        return;

    do
    {
        swapped = 0;
        ptr2 = head;

        while (ptr2->next != lptr2)
        {
            if (ptr2->CGPA < ptr2->next->CGPA)
            {
                swap(ptr2, ptr2->next);
                swapped = 1;
            }
            ptr2 = ptr2->next;
        }
        lptr2 = ptr2;
    }
    while (swapped);
}

//-------------------------------------------------------------------------------------------------------------------------------------------------

/* function to swap data of two nodes a and b*/
void swap(struct list *a, struct list *b)
{
    float temp = b->CGPA;
    b->CGPA = a->CGPA;
    a->CGPA = temp;

    char temp2[10];
    strcpy(temp2,b->reg_no);
    strcpy(b->reg_no,a->reg_no);
    strcpy(a->reg_no,temp2);


    char temp3[30];
    strcpy(temp3, b->name);
    strcpy(b->name,a->name);
    strcpy(a ->name,temp3);
}

//-------------------------------------------------------------------------------------------------------------------------------

void asking_for_mens_hostel()
{
    struct list *temp4=front;

    printf("\n\t\t ~~MEN'S HOSTEL ALLOTMENT~~\n\n");
    while (temp4->next!=NULL)
    {
        printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp4->name,temp4->reg_no,temp4->CGPA);
        block_name();
        room_number();
        temp4=temp4->next;
    }

        printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp4->name,temp4->reg_no,temp4->CGPA);
        block_name();
        room_number();

}

//-----------------------------------------------------------------------------------------------------------------------------

void asking_for_womens_hostel()
{
    struct list *temp4=head;

    printf("\n\t\t ~~WOMEN'S HOSTEL ALLOTMENT~~\n\n");
    while (temp4->next!=NULL)
    {
        printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp4->name,temp4->reg_no,temp4->CGPA);
        block_name();
        room_number();
        temp4=temp4->next;
    }

        printf("\nName: %s\nRegistration Number: %s\nCGPA: %f\n",temp4->name,temp4->reg_no,temp4->CGPA);
        block_name();
        room_number();
}
//------------------------------------------------------------------------------------------------------------------------------

void available()
{
    printf("\nThe available blocks for MEN'S HOSTEL are:- \n\t");
}

//-------------------------------------------------------------------------------------------------------------------------------

int main()
{
    int R,j,m,k;
    printf("\n\t\t\tWelcome to Hostel Counseling.\n\n");
    while (j=1)
    {
        printf("\n\t(1) Fill Student information\n\t(2) Rank List\n\t(3) Choose Hostel Block \n\t(4) Exit");
        printf("\nEnter your choice: ");
        scanf("%d",&m);

        switch(m)
        {
        case 1:
            details();
            break;

        case 2:
            printf("\n=============================================================================");
            bubbleSort();
            display();
            printf("\n=============================================================================");
            break;

        case 3:
            bubbleSort();
            asking_for_mens_hostel();
            asking_for_womens_hostel();
            break;

        case 4:
            exit(0);
        }
    }
    //R=room_number();
    //printf("\nThe room alloted to you is:- %d",R);
}
