//This my code, hope you have understand, if any queries post it in the comments.




















#include<bits/stdc++.h>
using namespace std;

class shopping
{
	private:
		int pcode;
		float discount,price;
		string name;
	public:
		void menu();
		void list();
		void administrator();
		void buyer();
		void add();
		void removep();
		void edit();
		void receipt();
};

void shopping::menu()
{
	m:
	cout<<"\t\t_________________________________\n";
	cout<<"\t\t                                 \n";
	cout<<"\t\t       SuperMarket Main Menu     \n";
	cout<<"\t\t                                 \n";
	cout<<"\t\t_________________________________\n";
	
	int choice;
	string email,password;
	
	cout<<"\t\t   ||  1) Administrator  ||\n";
	cout<<"\t\t   ||  2) Buyer          ||\n";
	cout<<"\t\t   ||  3) Exit           ||\n";
	cout<<"Enter your choice\n";
	cin>>choice;
	
	switch(choice)
	{
		case 1:
			cout<<"Enter your email to Login\n";
			cin>>email;
			cout<<"Please enter your passowrd\n";
			cin>>password;
			if(email=="vivek123@gmail.com" && password=="12345678")
			{
				cout<<"Successfully logged in!!!\n";
				administrator();
			}
			else
			{
				cout<<"Incorrect Email / Password\n";
			}
			break;
		case 2:
			cout<<"((((((Welcome Buyer))))))\n";
			buyer();
		case 3:
			exit(1);
		default:
			cout<<"Enter correct choice\n";
	}
	goto m;
}

void shopping::administrator()
{
	m:
	int choice;
	
	cout<<" ___________________\n";
	cout<<"                    \n";
	cout<<"|   Administrator   |\n";
	cout<<" ___________________\n";
	cout<<"\n";
	cout<<"| 1) Add an item in the menu    |\n";
	cout<<"| 2) Modify an item in the menu |\n";
	cout<<"| 3) Delete an item in the menu |\n";
	cout<<"| 4) Back to Main Menu          |\n";
	cout<<"| 5) Exit.                      |\n";
	cout<<"Please Enter your choice: ";
	cin>>choice;
	
	switch(choice)
	{
		case 1:
			add();
			break;
		case 2:
			edit();
			break;
		case 3:
			removep();
			break;
		case 4:
			menu();
			break;
		case 5:
			exit(1);
		default:
			cout<<"Enter the correct choice\n";
	}
	goto m;
}

void shopping::buyer()
{
	m:
	int choice;
	cout<<" ___________\n";
	cout<<"|   Buyer   |\n";
	cout<<" ___________\n";
	cout<<"| 1) Buy a product     |\n";
	cout<<"| 2) Back to Main Menu |\n";
	cout<<"Please Enter your choice: ";
	cin>>choice;
	
	switch(choice)
	{
		case 1:
			receipt();
			break;
		case 2:
			menu();
		default:
			cout<<"Enter the correct choice\n";
	}
	goto m;
}

void shopping::add()
{
	m:
	fstream data;
	int c;
	int token = 0;
	string n;
	float p,d;
	
	cout<<"Write the Code of the Product\n";
	cin>>pcode;
	cout<<"Write the Name of the Product\n";
	cin>>name;
	cout<<"Write the Price of the Product\n";
	cin>>price;
	cout<<"Write the Discount of the Product\n";
	cin>>discount;
	
	data.open("database.txt",ios::in);
	
	if(!data)
	{
		data.open("database.txt",ios::app|ios::out);
		data<<" "<<pcode<<" "<<name<<" "<<price<<" "<<discount<<"\n";
		data.close();
	}
	else
	{
		data>>c>>n>>p>>d;
		while(!data.eof())
		{
			if(c==pcode)
			{
				token++;
			}
			data>>c>>n>>p>>d;
		}
		data.close();
		
		if(token==1)
	    {
		    cout<<"The product Code already exist\n";
		    goto m;
	    }
	    else
	    {
		    data.open("database.txt",ios::app|ios::out);
		    data<<" "<<pcode<<" "<<name<<" "<<price<<" "<<discount<<"\n";
		    data.close();
	    }
	}
	cout<<"Product Added Successfully !!!\n";
}

void shopping::edit()
{
	fstream data,data1;
	int c,token=0,key;
	string n;
	float p,d;
	
	cout<<"||Modifying the product||\n";
	cout<<"Enter code of the Product\n";
	cin>>key;
	
	data.open("database.txt",ios::in);
	if(!data)
	{
		cout<<"File doesnot exist\n";
	}
	else
	{
		data1.open("database1.txt",ios::app|ios::out);
		data>>pcode>>name>>price>>discount;
		
		while(!data.eof())
		{
			if(key==pcode)
			{
				cout<<"Enter new code of the Product\n";
				cin>>c;
				cout<<"Enter new Name of the Product\n";
				cin>>n;
				cout<<"Enter new Price of the Product\n";
				cin>>p;
				cout<<"Enter new Discount Rate of the Product\n";
				cin>>d;
				data1<<" "<<c<<" "<<n<<" "<<p<<" "<<d;
				cout<<"\nThe record has been edited successfully!!\n";
				token++;
			}
			else
			{
				data1<<" "<<pcode<<" "<<name<<" "<<price<<" "<<discount<<endl;
			}
			data>>pcode>>name>>price>>discount;
		}
		if(token==0)
		{
			cout<<"No such item found!!\n";
		}
		data.close();
		data1.close();
		
		remove("database.txt");
		rename("database1.txt","database.txt");
	}
}

void shopping::removep()
{
	fstream data,data1;
	int key,token=0;
	
	cout<<"Enter the code of product to be deleted\n";
	cin>>key;
	
	data.open("database.txt",ios::in);
	if(!data)
	{
		cout<<"Cannot find the file\n";
	}
	else
	{
		data1.open("database1.txt",ios::app|ios::out);
		data>>pcode>>name>>price>>discount;
		while(!data.eof())
		{
			if(key==pcode)
			{
				cout<<"Product deleted successfuly\n";
				token++;
			}
			else
			{
				data1<<" "<<pcode<<" "<<name<<" "<<price<<" "<<discount<<"\n";
			}
			data>>pcode>>name>>price>>discount;
		}
		data.close();
		data1.close();
		
		remove("database.txt");
		rename("database1.txt","database.txt");
		if(token==0)
		{
			cout<<"\nProduct Not found!!!\n";
		}
	}
}

void shopping::list()
{
	fstream data;
	data.open("database.txt",ios::in);
	
	cout<<"\n--------------------------------------\n";
	cout<<"ProNo.\t\tName\t\tPrice";
	cout<<"\n--------------------------------------\n";
	data>>pcode>>name>>price>>discount;
	
	while(!data.eof())
	{
		cout<<pcode<<"\t\t"<<name<<"\t\t"<<price<<endl;
		data>>pcode>>name>>price>>discount;
	}
	data.close();
}

void shopping::receipt()
{
	fstream data;
	int c=0;
	char choice='Y';
	float amount=0,dis=0,total=0;
	int acode[100],quantity[100];
	
	cout<<"\t\tReceipt\n";
	data.open("database.txt",ios::in);
	if(!data)
	{
		cout<<"File not found!!\n";
	}
	else
	{
		data.close();
		list();
		cout<<"\n____________________________________\n";
		cout<<"                                      \n";
		cout<<"        Please Make your Order        \n";
		cout<<"\n____________________________________\n";
		do
		{
			m:
			cout<<"Enter Code of the product\n";
		    cin>>acode[c];
		    cout<<"Enter the quantity of product\n";
		    cin>>quantity[c];
		    for(int i=0;i<c;i++)
		    {
		    	if(acode[c]==acode[i])
		    	{
		    		cout<<"Duplicate product code.|| Please Try Again|\n";
		    		goto m;
				}
			}
			c++;
			cout<<"\nDo you want to buy another product?\n";
			cout<<"Press 'Y' to buy else 'N'\n";
			cin>>choice;
		}
		while(choice=='Y');
		
		cout<<"\tSr.No\tProduct_Name\tProduct_quantity\tPrice\tAmount\tAmount_with_discount\n";
		
		for(int i=0;i<c;i++)
		{
			data.open("database.txt",ios::in);
			data>>pcode>>name>>price>>discount;
			while(!data.eof())
			{
				if(pcode==acode[i])
				{
					amount = price*quantity[i];
					dis = amount - (amount*discount/100);
					total+=dis;
					cout<<"\n"<<pcode<<"\t\t"<<name<<"\t\t"<<quantity[i]<<"\t\t"<<price<<"\t\t"<<amount<<"\t\t"<<dis;
				}
				data>>pcode>>name>>price>>discount;
			}
		}
		data.close();
	}
	cout<<"\n___________________________________________________________________\n";
	cout<<"     || Total Amount : "<<total<<" Rs  ||\n";
	cout<<"\n___________________________________________________________________\n";
}

int main()
{
	shopping s;
	s.menu();
	//return 0;
}
