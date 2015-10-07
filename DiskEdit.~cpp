//---------------------------------------------------------------------------
#include <iostream>
#include <windows.h>
#include <fstream.h>

#include <vcl.h>
#pragma hdrstop

#include "DiskEdit.h"
//---------------------------------------------------------------------------
#pragma package(smart_init)
#pragma resource "*.dfm"
//---------------------------------------------------------------------------
   //Disk
   /*
    typedef struct _DISK_GEOMETRY
    {
        LARGE_INTEGER Cylinders; // Количество цилиндров
        DWORD MediaType;
        DWORD TracksPerCylinder; // Количество дорожек на цилиндр
        DWORD SectorsPerTrack;  // Количество секторов на дорожку
        DWORD BytesPerSector;
    }   DISK_GEOMETRY;         */

    DISK_GEOMETRY diskGeometry;

    DWORD bytesReturned=0;

    BYTE *buffer=NULL;

    DWORD bufferSize;

    BOOL result=0;
//---------------------------------------------------------------------------
TForm1 *Form1;
//---------------------------------------------------------------------------
__fastcall TForm1::TForm1(TComponent* Owner)
   : TForm(Owner)
{
//   SaveDialog1->DefaultExt = "*.av22";
//   SaveDialog1->Filter = "AV22 КЗА файлы (*.av22)";
}
//-----------------------------------------------------------------------------
void TForm1::SaveSektorToFile(String FileName)
{

}

void  TForm1::DriveRead(void)
{
    String DriveOpen="\\\\.\\"+DriveComboBox1->Items->Strings[DriveComboBox1->ItemIndex];
    DriveOpen.Insert('\0',7);
    wchar_t wstr[10] = {'\0'};
    swprintf(wstr, L"%S", DriveOpen.c_str());
    HANDLE hFile=CreateFileW(wstr ,GENERIC_READ, FILE_SHARE_READ | FILE_SHARE_WRITE,0,OPEN_EXISTING,0,0);
    if (hFile==INVALID_HANDLE_VALUE)
    {
       int err = GetLastError();
       ShowMessage("Ошибка #" + IntToStr(err) + ": Не удалось открыть диск!");
       CloseHandle(hFile);
       return;
    }

    DeviceIoControl(hFile,IOCTL_DISK_GET_DRIVE_GEOMETRY,NULL,0,&diskGeometry,sizeof (DISK_GEOMETRY),&bytesReturned,(LPOVERLAPPED)NULL);

    StringGrid1->RowCount=diskGeometry.BytesPerSector/16+1;

    bufferSize=diskGeometry.BytesPerSector;

    buffer = new BYTE[bufferSize];
    SetFilePointer(hFile,StrToInt(Edit1->Text)*bufferSize,NULL,FILE_BEGIN);
    result = ReadFile(hFile, buffer, bufferSize, &bytesReturned, 0);
    if (!result)
    {
       int err = GetLastError();
       ShowMessage("Ошибка #" + IntToStr(err));
       delete[] buffer;
       CloseHandle(hFile);
       return;
    }
    cout << buffer;
    //system("pause");
    String txt;
    StringGrid1->RowCount = (bufferSize/(int)(StringGrid1->ColCount-1))+1;
    int d_i=0;
    for (int i = 1; i < (int)StringGrid1->RowCount; i++)
       for (int j = 1; j < (int)StringGrid1->ColCount; j++){
            txt.sprintf("%x\n", j-1); StringGrid1->Cells[j][0] = txt;
            txt.sprintf("%x\n", (i-1)*(int)(StringGrid1->ColCount-1) + StrToInt(Edit1->Text)*bufferSize); StringGrid1->Cells[0][i] = txt;
            txt.sprintf("%x\n", buffer[((int)StringGrid1->ColCount-1)*(i-1)+(j-1)]); StringGrid1->Cells[j][i] = txt;
            d_i++;
            DataSektor[d_i] = buffer[((int)StringGrid1->ColCount-1)*(i-1)+(j-1)];
       }
    Label4->Caption = IntToStr(diskGeometry.MediaType);
    Label2->Caption = IntToStr(diskGeometry.TracksPerCylinder);
    Label6->Caption = IntToStr(diskGeometry.SectorsPerTrack);
    Label8->Caption = IntToStr(diskGeometry.BytesPerSector);
    Label14->Caption = IntToStr(diskGeometry.Cylinders.QuadPart);
    CloseHandle(hFile);
}
//---------------------------------------------------------------------------
  

void __fastcall TForm1::FormResize(TObject *Sender)
{
     StringGrid1->Width = Form1->Width-230;
     StringGrid1->Height = Form1->Height-90;
     Panel1->Left = Form1->Width - 220;
     Panel2->Left = Form1->Width - 220;
     Memo1->Left = Form1->Width - 220;
}
//---------------------------------------------------------------------------
void __fastcall TForm1::Button1Click(TObject *Sender)
{
   DriveRead();
}
//---------------------------------------------------------------------------
void __fastcall TForm1::Button2Click(TObject *Sender)
{
   SaveDialog1->Execute();
   int a,b;
   a = StrToInt(Edit2->Text);
   b = StrToInt(Edit3->Text);
   if(a>b)
   {
      int tmp;
      tmp = a;
      a=b;
      b=tmp;
   }
   fstream file;
   file.open(SaveDialog1->FileName.c_str(), ios:: out | ios::binary);
   if (!file)
   {
      String txt = "Запись не удалась сюда: ";
      txt += SaveDialog1->FileName.c_str();
      Application->MessageBoxA(txt.c_str(),"Опаньки :(",0);
      return;
   }
   else
   {
      for(int i=a; i<=b; i++)
      {
         Edit1->Text = i;
         DriveRead();
         file.write(buffer, bufferSize);
         ProgressBar1->Position = (i*100)/(b-a);
      }
      String txt = "Запись удалась сюда: ";
      txt += SaveDialog1->FileName.c_str();
      Application->MessageBoxA(txt.c_str(),"Внимание",0);
   }
   file.close();
}
//---------------------------------------------------------------------------

void __fastcall TForm1::Edit1KeyPress(TObject *Sender, char &Key)
{
    if(Key==13)
    {
      DriveRead();
    }
}
//---------------------------------------------------------------------------

void __fastcall TForm1::Button3Click(TObject *Sender)
{
   Memo1->Visible = !Memo1->Visible;  
}
//---------------------------------------------------------------------------

