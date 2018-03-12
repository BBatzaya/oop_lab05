#include <iostream>
#include<stdbool.h>
#include<iomanip>
#include<cstring>
using namespace std;
int h = 0, k = 0;
class employee{
    //private хандалтын түвшинтэй ажилтны 4н гишүүн өгөгдөл, 1 гишүүг функц зарлаж байна.
private:
    int number;
    char name[20];
    char ajil[20];
    float time;
    float zahirliin(float);
    //public хандалтын түвшинтэй ажилтны мэдээллийн боловсруулах гишүүн функц зарлаж байна.
public:
    void setdata();
    void getdata();
    float timeSum(float &);
    float showData();
    void update(employee &a);
};
//menu дэлгэцлэх функц.
void head()
{
    cout << "1.ajiltnii medeelel oruulah " << "\n";
    cout << "2.tsalin bodoh" << "\n";
    cout << "3. ajillasan tsag nemeh " << "\n";
    cout << "4.hevleh"<< "\n";
    cout << "5.Sort"<< "\n";
    cout << "6.Exit"<< "\n";
}
//объектынх аа гишүүн өгөгдөлрүү гараас утга оноохын тулд классын getData гэсэн функцад хандан онооно.
void employee::getdata()
{
    number = ++h;
    cout << "Number: " << number << "\n";
    cout << "name: ";   cin >> name;
    cout << "ajil: ";   cin >> ajil;
    cout << "time: ";   cin >> time;
}

float employee::zahirliin(float m)
{
    return 100000 + 5000*m;
}
//ажилтны цалинг бодохын тулд классын showData гишүүн функцруу хандсанаар ажилласан цаг гэсэн гишүүн өгөгдөлрүү хандаж байна.
float employee::showData()
{
    //нэг класс дахь public түвшний гишүүн функцээр хандаж байгаа учир гишүүн өгөгдөлд шууд хандаж ажилтны албан тушаалыг шалгаж байна.
    if(0 == strcmp("zahiral", ajil)) return zahirliin(time);
    else return 5000*time;
}
//ажилтны ажилласан цагийг бодохын тулд классын гишүүн функцруу хандсанаар ажилласан цаг гэсэн гишүүн өгөгдөлрүү хандаж байна.
float employee::timeSum(float &ax)
{
    //гараас оруулсан нэмэх цагны утга 24 өөс 0 ийн хооронд байх ёстой.
    if(ax <= 24 && ax > 0)
    {time = time + ax; return true;}
    else return false;//хэрэв 24 өөс их 0 ээс бага тоо оруулсан бол 0 гэсэн утга буцаана.
}
void employee::setdata()
{
    cout << setw(3) << number << setw(12) << name << setw(12) << ajil << setw(6) << time << setw(10) <<"\n" ;
}
//ажилтны цалингаар нь эрэмбэлэх функц
void sortTime(employee a[], int m)
{
    for(int j = 0; j < m; j++)
    {
        for(k = 0; k < m -j - 1; k++)
        {
            //эхний ажилтны цалин дараагын ажилтны цалингаас бага гэдгийг шалгах
            if(a[k].showData() < a[k+1].showData() )
            {
                a[k].update(a[k+1]);//үнэн бол байр солих функцрууу хандана
            }
        }
    }
}


//2 ажилтны байр солих функц
void employee::update(employee &a)
{
    char change[20];
    strcpy(change,name);
    strcpy(name,a.name);
    strcpy(a.name,change);
    float changee;
    changee = time;
    time = a.time;
    a.time = changee;
    char z1[20];
    strcpy(z1,ajil);
    strcpy(ajil,a.ajil);
    strcpy(a.ajil,z1);
}
int main()
{
    int n = 0, b = 0, i, j;
    float c;
    employee *a1;
    a1 = new employee[100];
    head(); //menu дэлгэцлэх функц.
    while(b != 6)
    {
        cout << "> "; cin >> b;
        if(b == 1){
            cout << "heden ajiltnii medeelel oruulah ve? "; cin >> n;
            for(i = 0;i < n; i++)
                a1[i].getdata();//ажилтны мэдээллийг гараас оруулахын тулд объектоор нь read гэсэн гишүүн функцад хандаж байна.
        }
        if(b == 2)
            for(i = 0, j = i;i < n; i++)
                cout << ++j << " dugaartai ajiltnii tsalin: "<< a1[i].showData() << "\n"; //ажилтны цалинг бодохын тулд объектоор нь showData гэсэн гишүүн функцад хандаж байна.
        if(b == 3)
        {
            cout << "nemeh tsagaa oruulna uu? "; cin >> c;
            for(i = 0, j = i;i < n; i++)
            {
                //ажилласан цаг нэмэгдүүлэхийн тулд объектоор нь timesum гэсэн гишүүн функцад хандаж, нэмэх цагаа дамжуулж байна.
                if( 1 == a1[i].timeSum(c)) cout << ++j << "dugaartai ajiltnii tsag nemelt AMJILTTAI nemegdlee" << "\n";
                else cout << ++j << "dugaartai ajiltnii tsag nemelt AMJILTGUI..." << "\n";
            }
        }
        if(b == 4)
        {
            for(i = 0;i < n; i++)
                a1[i].setdata();//гараас оруулсан мэдээллээ хэвлэхийн тулд объектоор нь setdata гэсэн гишүүн функцад хандаж байна.
        }
        if(b == 5)
            sortTime(a1, n);//ажилтны цалингаар нь эрэмбэлэх функцад хандаж байна.
    }
    delete[]a1;
}



