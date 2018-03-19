#include <iostream>
#include<stdbool.h>
#include<iomanip>
#include<cstring>
using namespace std;
int h = 0, k = 0;
class employee{
    //private хандалтын түвшинтэй ажилтны 4н гишүүн өгөгдөл, 1 гишүүг функц зарлаж байна.
private:
    int id;
    char name[20];
    char ajil[20];
    float time;
    float zahirliin(float);
    //public хандалтын түвшинтэй ажилтны мэдээллийн боловсруулах гишүүн функц зарлаж байна.
public:
    employee();
    employee(int , char *, char *, float );
    void setdata();
    void getdata();
    bool before(employee &a);
    bool idshalgah( int);
    float timeSum(float &);
    float showData();
    void update(employee &a);
    void updatename(employee &a);
    // ~employee();
};
//menu дэлгэцлэх функц.
void head()
{
    cout << "1.ajiltnii medeelel oruulah " << "\n";
    cout << "2.tsalin bodoh" << "\n";
    cout << "3. ajillasan tsag nemeh " << "\n";
    cout << "4.hevleh"<< "\n";
    cout << "5.Sort"<< "\n";
    cout << "6.SortName"<< "\n";
    cout << "7.Exit"<< "\n";
}
employee a2[5];//шинэ ажилтан оруулахдаа ID давхцуулахгүй байлгахын тулд оруулж байгаа ажилтан бүрийн зөвхөн ID оруулна.
employee::employee()
{
    char n[17], m[17];
    id = 1;
    a2[h].id = 1;
    strcpy(m, "Bat");
    name = new char[strlen(m)+1];
    strcpy(name, m);
    strcpy(n, "ajil");
    ajil = new char[strlen(n)+1];
    strcpy(ajil, n);
    time = 120;
    h++;
}
bool employee::idshalgah(int y)
{
    if(id == y)
    return true;
    else return false;
}
employee::employee(int x, char *n, char *m, float y)
{
    id = x;
    a2[h].id = x;
    name = new char[strlen(n)+1];
    strcpy(name, n);
    ajil = new char[strlen(n)+1];
    strcpy(ajil, m);
    time = y;
    h++;
}
/*employee::~employee()
{
    cout<<"The object "<< name << ajil <<" is deleted;"<<endl;
    delete name;
    delete ajil;
}*/
//объектынх аа гишүүн өгөгдөлрүү гараас утга оноохын тулд классын setData гэсэн функцад хандан онооно.
/*void employee::setdata()
{
    id = ++h;
    cout << "id: " << id << "\n";
    cout << "name: ";   cin >> name;
    cout << "ajil: ";   cin >> ajil;
    cout << "time: ";   cin >> time;
}*/
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
void employee::getdata()
{
    cout << setw(3) << number << setw(12) << name << setw(12) << ajil << setw(6) << time << setw(10) <<"\n" ;
}
bool employee::before(employee &a)
{
    if(strcmp(name,a.name) >= 0)
    return true;
    else return false;
}

void sortName(employee a[], int m)
{
    for(int j = 0; j < m; j++)
    {
        for(k = 0; k < m -j - 1; k++)
        {
            if(a[k].before(a[k+1]) == 1)
            {
                a[k].updatetime(a[k+1]);
            }
        }
    }
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
void employee::updatename(employee &a)
{
    int q;
    q = id;
    id = a.id;
    a.number = q;
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
    int b = 0, i = 0, j, g, id1;
    char name1[17], ajil1[17];
    float c, time1;
    a1 = new employee[5];
    a1[i] = employee();
    for(i = 1; i < 5; i++)
    {
        cout << "id: "; cin >> id1;
        cout << "Name: ";   cin >> name1;
        cout << "Ajil: ";   cin >> ajil1;
        cout << "Time: ";   cin >> time1;
        int key = 0;
        for(g = 0; g < h; g++)
        {
            if(a2[g].idshalgah(id1))
            {
                key++;
                break;
            }
        if(key == 0)
        {
            a1[i] = employee(id1, name1, ajil1, time1);
        }else
        {
                cout << "ID-giin dugaar dawhtsaj bna.";
                i--;
        }
    }
    head(); //menu дэлгэцлэх функц.
    while(b != 7)
    {
        cout << "> "; cin >> b;
       /* if(b == 1){
            cout << "heden ajiltnii medeelel oruulah ve? "; cin >> n;
            for(i = 0;i < n; i++)
                a1[i].getdata();//ажилтны мэдээллийг гараас оруулахын тулд объектоор нь read гэсэн гишүүн функцад хандаж байна.
        }*/
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
                a1[i].getdata();//гараас оруулсан мэдээллээ хэвлэхийн тулд объектоор нь setdata гэсэн гишүүн функцад хандаж байна.
        }
        if(b == 5)
            sortTime(a1, n);//ажилтны цалингаар нь эрэмбэлэх функцад хандаж байна.
        if(b == 6)
            for(i = 0;i < 5; i++)
                sortName(a1, 5);
    }
    delete[]a1;
}



