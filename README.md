# linkedlist.project

#include<stdio.h>
#include<stdlib.h>


#define NULL_VALUE -99999
#define SUCCESS_VALUE 99999

struct listNode
{
    int item;
    struct listNode * next;
};

struct listNode * list;

void initializeList()
{
    list = 0;  //initially set to NULL
}

int insertItem(int item) //insert at the beginning
{
	struct listNode * newNode ;
	newNode = (struct listNode*) malloc (sizeof(struct listNode)) ;
	newNode->item = item ;
	newNode->next = list ; //point to previous first node
	list = newNode ; //set list to point to newnode as this is now the first node
	return SUCCESS_VALUE ;
}


int deleteItem(int item)
{
	struct listNode *temp, *prev ;
	temp = list ; //start at the beginning
	while (temp != 0)
	{
		if (temp->item == item) break ;
		prev = temp;
		temp = temp->next ; //move to next node
	}
	if (temp == 0) return NULL_VALUE ; //item not found to delete
	if (temp == list) //delete the first node
	{
		list = list->next ;
		free(temp) ;
	}
	else
	{
		prev->next = temp->next ;
		free(temp);
	}
	return SUCCESS_VALUE ;
}


struct listNode * searchItem(int item)
{
	struct listNode * temp ;
	temp = list ; //start at the beginning
	while (temp != 0)
	{
		if (temp->item == item) return temp ;
		temp = temp->next ; //move to next node
	}
	return 0 ; //0 means invalid pointer in C, also called NULL value in C
}

void printList()
{
    struct listNode * temp;
    temp = list;
    while(temp!=0)
    {
        printf("%d->", temp->item);
        temp = temp->next;
    }
    printf("\n");
}

int insertLast(int item)
{
    struct listNode *temp,*prev,*newNode;
    temp=list;
    newNode = (struct listNode*) malloc (sizeof(struct listNode)) ;
	newNode->item = item ;
	newNode->next=0;
    while(temp!=0)
    {   prev=temp;
        temp=temp->next;
    }
    prev->next=newNode;


}

int insertAfter(int oldItem, int newItem)
{
    struct listNode *temp,*newnode,*prev;
    newnode = (struct listNode*) malloc (sizeof(struct listNode)) ;
    temp=list;
    newnode->item=newItem;
    while(temp!=0)
    {
        if(temp->item==oldItem)
            break;
        temp=temp->next;
    }
    newnode->next=temp->next;
    temp->next=newnode;


}

int deleteLast()
{
struct listNode *temp,*prev,*prev2;
temp=list;
while(temp->next!=0)
{   prev=temp;
    temp=temp->next;
}
prev->next=0;
free(temp);

return SUCCESS_VALUE;
}

int deleteFirst()
{   struct listNode *temp;
    temp=list;
    list=list->next;
    free(temp);
}


int main(void)
{
    initializeList();
    while(1)
    {
        printf("1. Insert new item. 2. Delete item. 3. Search item. \n");
        printf("4. (Add from homework). 5. Print. 6. exit.\n");
        printf("7.insertLast 8.insertAfter 9.deleteFirst 10.delete last\n");

        int ch;
        scanf("%d",&ch);
        if(ch==1)
        {
            int item;
            scanf("%d", &item);
            insertItem(item);
        }
        else if(ch==2)
        {
            int item;
            scanf("%d", &item);
            deleteItem(item);
        }
        else if(ch==3)
        {
            int item;
            scanf("%d", &item);
            struct listNode * res = searchItem(item);
            if(res!=0) printf("Found.\n");
            else printf("Not found.\n");
        }
        else if(ch==5)
        {
            printList();
        }
        else if(ch==6)
        {
            break;
        }
        else if(ch==7)
        {   int n;
            scanf("%d",&n);
            insertLast(n);
        }
        else if(ch==8)
        {
            int old,nw;
            scanf("%d%d",&old,&nw);
            insertAfter(old,nw);
        }
        else if(ch==9)
        {
            deleteFirst();
        }
        else if(ch==10)
        {
            deleteLast();
        }
    }

}
