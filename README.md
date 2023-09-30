# test_9_30
#include <stdio.h>
#include <stdlib.h>
//队列的链式存储
typedef struct LinkNode{
	ElemType data;
	struct LinkNode* next;
}LinkNode;
typedef struct{
	LinkNode *front,*rear;
}LinkQueue;

void InitQueue(LinkQueue &Q){
	Q.front = Q.rear = (LinkNode*)malloc(sizeof(LinkNode));
	Q.front->next = NULL;
}
bool QueueEmpty(LinkQueue Q){
	if(Q.front == Q.rear)
		return true;
	else
		return false;
}
void EnQueue(LinkQueue &Q,int x){
	LinkNode* s = (LinkNode*)malloc(sizeof(LinkNode));
	s->data = x;
	s->next = NULL;
	//带头结点
	//if(Q.front == NULL)
	//Q.front = Q.rear = s;
	//else
	Q.rear->next = s;
	Q.rear = s;
}
bool DeQueue(LinkQueue &Q,int &x){
	//带头结点
	if(Q.front == Q.rear)
		return false;
	LinkNode* p = Q.front->next;
	x = p->data;
	Q.front->next = p->next;
	if(Q.rear == p)
		Q.front = Q.rear;
	free(p);
	return true;
	//不带头结点
	if(Q.front == NULL)
		return false;
	LinkNode* p = Q.front;
	x = p->data;
	Q.front = p->next;
	if(Q.rear == p)
		Q.front = Q.rear = NULL;
	free(p);
	return true;
}
//求队长
int Length(LinkQueue &Q){
	int Len = 0;
	while(Q.front->next != NULL && Q.front != Q.rear){
		Q.front = Q.front->next;
		Len++;
	}
	return Len;
}
void testQueue(){
	LinkQueue Q;
	InitQueue(&Q);
	QueueEmpty(Q);
	EnQueue(&Q,x);
	DeQueue(&Q,&x);
}
