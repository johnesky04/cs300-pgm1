# cs300-pgm1
data structure repository
// File name: pgm1.cpp
// Author: John Ebeigbe
// Assignment Number: 1
// Description:  Keeping track of my inventory.
// Last Updated: september 19 2016.

#include <iostream>
#include <fstream>
#include <string>

using namespace std;

class part
 {
 public:
     int partNum;
     string description;
     int quantity;
     float unitprice;
 };
 
 void printAllParts(part [], int);
 void addPart(part [], int&);
 void modifyPart(part [], int);
 
 
 int main()
 {
     
     part arr[100];     // this is the array to hold objects.
     int count = 0;
     
     
     // lets write a menu
     int choice = 0;
     cout<<"Welcome to Tiny part mgmt"<<endl;
     cout<<"*************************"<<endl;
     cout<<"1. Print the part"<<endl;
     cout<<"2. Create a new part"<<endl;
     cout<<"3. Modify a part"<<endl;
     cout<<"4. Print total"<<endl;
     cout<<"5. Exit the program"<<endl;
     cout<<"Dear user please make a choice: ";
     cin>>choice;
     while (cin.good() && choice != 5)
     {
         switch (choice){
         case 1:
              printAllParts(arr, count);
              break;
         case 2:
              cin.ignore();
              addPart(arr, count);
              break;
         case 3:
              modifyPart(arr, count);
              break;
         case 4:
              {
               float total = 0;
               for(int h = 0; h < count; h++)
               {
                   total = (arr[h].unitprice * arr[h].quantity) + total;
                }
                  cout<<"Total cost of your inventory: "<<total<<endl;
              break;
          }
         case 5:
               {
                   std::fstream file("inventory.txt",std::ios::out);
                  
                   //if file is good then write the file
                   if(file)
                   {
                       for(int i = 0; i < count; i++)
                        {
                         int partNum=arr[i].partNum;
                         std::string description = arr[i].description;
                         int quantity = arr[i].quantity;
                         float unitprice = arr[i].unitprice;
                         
                         file<<partNum<<std::endl;
                         file<<description<<std::endl;
                         file<<quantity<<std::endl;
                         file<<unitprice<<std::endl;
                        }
                   }
                   else
                   {
                       std::cout<<"Error when writing to file \"inventory.txt\""<<std::endl;
                      }
                      //close file when done.
                      file.close();
                      break;
                  }
         default:
              cout<<"invalid choice"<<endl;
             
        }
        cout<<"Dear user please make a choice: "<<endl;
        cin>>choice;
       }
         
     return 0;
     
 }
     
     void printAllParts(part arr[], int count)
     {
         if (count == 0)
         {
             cout<<"Empty Inventory."<<endl;
             return;
         }
         for (int i = 0; i < count; i++)
         {
             cout<<"Part Number: "<<arr[i].partNum <<endl;
             cout<<"Description: "<<arr[i].description <<endl;
             cout<<"Quantity: "<<arr[i].quantity <<endl;
             cout<<"Unit Price: "<<arr[i].unitprice <<endl;
          }
         
        }
     void addPart(part arr[],int & count)
     {
         cout<<"New part description: "<<endl;
         string desc;
         getline(cin, desc);
         
         cout<<"New part quantity: ";
         int quantity =0;
         cin>> quantity;
         
         cout<<"New part unit price: ";
         float price =0;
         cin >> price;
         
         arr[count].partNum = count + 1;
         arr[count].description = desc;
         arr[count].quantity = quantity;
         arr[count].unitprice = price;
         count++;
         
        }
     void modifyPart(part arr[], int count) //function that modifies parts
     {
         int mod = 0;
         cout<<"Enter part to modify: ";
         cin>>mod;
         mod = mod - 1;
         
         cout<<"New part description: "<<endl;
         string desc;
         cin.ignore();
         getline(cin, arr[mod].description);
         
         cout<<"New part quantity: "<<endl;
         cin>>arr[mod].quantity;
         
         cout<<"New part price: "<<endl;
         cin>>arr[mod].unitprice;
      }
