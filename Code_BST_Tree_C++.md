#include<iostream>
#include<stdio.h>
#include<cstdlib>
#include<conio.h>

using namespace std;
typedef int Data;
struct BSTNode
{
	Data Info;
	BSTNode *Left;
	BSTNode *Right;
};
typedef BSTNode *Tree;
	Tree T, T1;
	int Found = 0;
void InitTree(Tree &T)
{
	T = NULL;
}
	int Empty(Tree T)
{
	return (T==NULL?1:0);
}
void InsertNode(Data x, Tree &T)
{
	if(T==NULL)
	{
		Tree p = new BSTNode;
		p->Info = x;
		p->Left = p->Right = NULL;
		p->Left = p->Right = NULL;
		T = p;
	}
		else if(T->Info>x) InsertNode(x,T->Left);
		 	else InsertNode(x,T->Right);
}
void CreateTree(Tree &T)
{
	Data x;
	InitTree(T);
	do{
		cout<<"Nhap 1 gia tri, nhap 0 de dung: ";
		cin>>x;
		if(x!=0)
			InsertNode(x,T);
	}while(x!=0);
}
void NLR(Tree T)
{
	if(!Empty(T))
	{
		cout<<T->Info<<" ";
		NLR(T->Left);
		NLR(T->Right);
	}
}
void LNR(Tree T)
{
	if(!Empty(T))
	{
		LNR(T->Left);
		cout<<T->Info<<" ";
		LNR(T->Right);
	}
}
void LRN(Tree T)
{
	if(!Empty(T))
	{
		LRN(T->Left);
		LRN(T->Right);
		cout<<T->Info<<" ";
	}
}
Tree Seach(Data x, Tree T)
{
	if(!Empty(T))
		{
			if(x==T->Info) return T;
			if(x<T->Info) return Seach(x,T->Left);
			else return Seach(x,T->Right);
		}
	return NULL;
}
void Tim2so(Data M, Tree T)
{
	if(T!=NULL)
	{
		int L = T->Info;
		if(L<M)
		{
		int K;
			K = M - L;
			Tree p = Seach(K,T1);
			if(p!=NULL && L>K) 
				{
					cout<<L<<"+"<<K<<"="<<M<<"\n";
					Found = 1;
				}
		}
		Tim2so(M,T->Left);
		Tim2so(M,T->Right);
	}
}
int DemNodeLa(Tree T)
{
	if(Empty(T)) return 0;
	else
	{
		if(T->Left==NULL && T->Right==NULL)
			return 1;
		else return DemNodeLa(T->Left) + DemNodeLa(T->Right);
	}
}
int DemNode1Con(Tree T)
{
	if(Empty(T)) return 0;
	else
	{
		if((T->Left==NULL && T->Right!=NULL) || (T->Left!=NULL && T->Right==NULL))
			return 1 + DemNode1Con(T->Left) + DemNode1Con(T->Right);
			else return DemNode1Con(T->Left) + DemNode1Con(T->Right);
	}
}
int DemNode2Con(Tree T)
{
	if(Empty(T)) return 0;
	else
	{
		if(T->Left!=NULL && T->Right!=NULL)
			return 1 + DemNode2Con(T->Left) + DemNode2Con(T->Right);
		else return DemNode2Con(T->Left) + DemNode2Con(T->Right);
	}
}
int ChieuCao(Tree T)
{
	if(Empty(T)) return 0;
	else
	{
		if(ChieuCao(T->Left)>ChieuCao(T->Right))
			return 1 + ChieuCao(T->Left);
		else return 1 + ChieuCao(T->Right);
	}
}
void InNutMuck(Data m, Data k, Tree T)
{
	if(Empty(T)) return;
	else
	{
		if(m==k) cout<<T->Info<<" ";
		else
		{
			m++;
			if(T->Left!=NULL) InNutMuck(m,k,T->Left);
			if(T->Right!=NULL) InNutMuck(m,k,T->Right);
		}
	}
}
void Menu()
{
	cout<<"----------Menu----------\n";
	cout<<"1.Khoi tao cay BST\n";
	cout<<"2.Duyet kieu NLR\n";
	cout<<"3.Duyet kieu LNR\n";
	cout<<"4.Duyet kieu LRN\n";
	cout<<"5.Chen nut moi len cay\n";
	cout<<"6.Tim mot nut\n";
	cout<<"7.Tim 2 nut tren cay co tong bang so cho truoc\n";
	cout<<"8.Dem so nut la tren cay\n";
	cout<<"9.Dem so nut co dung 1 con\n";
	cout<<"10.Dem so nut co du 2 con\n";
	cout<<"11.Tinh chieu cao cay\n";
	cout<<"12.In cac nut o muc k\n";
	cout<<"0.Thoat\n";
	cout<<"------------------------\n";
}
int Chonmn()
{
	int n = 0;
	cout<<"\nMoi chon menu: ";
	cin>>n;
	if(n>0||n<13)
		return n;
	else return Chonmn();
}
void Xuly()
{
	int chon = Chonmn();
	switch(chon)
	{
		case 1: cout<<"1.Khoi tao cay BST\n";
			CreateTree(T);
		break;
		case 2: cout<<"2.Duyet kieu NLR\n";
			NLR(T);
		break;
		case 3: cout<<"3.Duyet kieu LNR\n";
			LNR(T);
		break;
		case 4: cout<<"4.Duyet kieu LRN\n";
			LRN(T);
		break;
		case 5: cout<<"5.Chen nut moi len cay\n";
			Data x;
			cout<<"Nhap nut can them: ";
			cin>>x;
			InsertNode(x,T);
		break;
		case 6: cout<<"6.Tim mot nut\n";
			cout<<"Nhap nut can tim: ";
			cin>>x;
			if(!Seach(x,T)) cout<<"Khong Tim thay";
			else cout<<"Tim thay";
		break;
		case 7: cout<<"7.Tim 2 nut tren cay co tong bang so cho truoc\n";
			cout<<"Nhap tong can tim: ";
			cin>>x;
			T1 = T;
			Tim2so(x,T);
			if(!Found) cout<<"Khong tim thay";
		break;
		case 8: cout<<"8.Dem so nut la tren cay\n";
			cout<<DemNodeLa(T);
		break;
		case 9: cout<<"9.Dem so nut co dung 1 con\n";
			cout<<DemNode1Con(T);
		break;
		case 10: cout<<"10.Dem so nut co du 2 con\n";
			cout<<DemNode2Con(T);
		break;
		case 11: cout<<"11.Tinh chieu cao cay\n";
			cout<<ChieuCao(T);
		break;
		case 12: cout<<"12.In cac nut o muc k\n";
			Data m, k;
			m = 0;
			cout<<"Nhap muc k: ";
			cin>>k;
			InNutMuck(m,k,T);
		break;
		case 0: exit(1);
		break;
	}
}
int main()
{
	Menu();
	while(true)
	{
		Xuly();
	}
	return 0;
}
