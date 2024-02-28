#include <iostream>
#include <fstream>
#include <string>
using namespace std;
const int record = 50;
const int waveData = 7;
double myArray[record][waveData] = {};
int main()
{
fstream fileReading;
fileReading.open("wavedata.txt");
if (fileReading)
{
cout << "Correct file path " << endl;
for (int r = 0; r < record; r++)
{
for (int c = 0; c < waveData; c++)
{
double value = 0;
if (fileReading >> value)
{
myArray[r][c] = value;
}
}
}
}
else
{
cout << "Incorrect file path " << endl;
}
cout << "Records with a greater then 1/7 steepness" << endl;
cout << "year\tmonth\tday\thour\tmin\t\twave height(m)\twave length(m)" << endl;
for (int r = 0; r < record; r++)
{
if ((myArray[r][5] / myArray[r][6]) > 1.0 / 7)
{
for (int c = 0; c < waveData; c++)
{
cout << myArray[r][c] << '\t' ;
if (c >= waveData - 3) {
cout << '\t';
}
}
cout << endl;
}
}
int heighPos = 5;
int lengthPos = 6;
double sum2010 = 0;
double sum2011 = 0;
double sum2012 = 0;
int numberOf2010s = 0;
int numberOf2011s = 0;
int numberOf2012s = 0;
double max2010 = myArray[0][heighPos] / myArray[0][lengthPos];
double max2011 = myArray[0][heighPos] / myArray[0][lengthPos];
double max2012 = myArray[0][heighPos] / myArray[0][lengthPos];
for (int r = 0; r < record; r++) {
if (myArray[r][0] == 2010) {
sum2010 += myArray[r][heighPos] / myArray[r][lengthPos];
numberOf2010s += 1;
if (max2010 < myArray[r][heighPos] / myArray[r][lengthPos]) {
max2010 = myArray[r][heighPos] / myArray[r][lengthPos];
}
}
else if (myArray[r][0] == 2011) {
sum2011 += myArray[r][heighPos] / myArray[r][lengthPos];
numberOf2011s += 1;
if (max2011 < myArray[r][heighPos] / myArray[r][lengthPos]) {
max2011 = myArray[r][heighPos] / myArray[r][lengthPos];
}
}
else if (myArray[r][0] == 2012) {
sum2012 += myArray[r][heighPos] / myArray[r][lengthPos];
numberOf2012s += 1;
if (max2012 < myArray[r][heighPos] / myArray[r][lengthPos]) {
max2012 = myArray[r][heighPos] / myArray[r][lengthPos];
}
}
}
cout << endl;
cout << " The average sum for 2010 steepness: " << sum2010 / numberOf2010s << ".
The highest steepness is: " << max2010 << endl;
cout << " The average sum for 2011 steepness: " << sum2011 / numberOf2011s << ".
The highest steepness is: " << max2011 << endl;
cout << " The average sum for 2012 steepness: " << sum2012 / numberOf2012s << ".
The highest steepness is: " << max2012 << endl;
return 0;
}
