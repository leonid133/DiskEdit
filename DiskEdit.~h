//---------------------------------------------------------------------------

#ifndef DiskEditH
#define DiskEditH
//---------------------------------------------------------------------------
#include <Classes.hpp>
#include <Controls.hpp>
#include <StdCtrls.hpp>
#include <Forms.hpp>
#include <FileCtrl.hpp>
#include <Grids.hpp>
#include <ComCtrls.hpp>
#include <ExtCtrls.hpp>
#include <Dialogs.hpp>
#include <jpeg.hpp>
//---------------------------------------------------------------------------
class TForm1 : public TForm
{
__published:	// IDE-managed Components
   TEdit *Edit1;
   TStringGrid *StringGrid1;
   TDriveComboBox *DriveComboBox1;
   TButton *Button1;
   TUpDown *UpDown1;
   TPanel *Panel1;
   TLabel *Label3;
   TLabel *Label4;
   TLabel *Label1;
   TLabel *Label2;
   TLabel *Label5;
   TLabel *Label6;
   TLabel *Label7;
   TLabel *Label8;
   TLabel *Label9;
   TPanel *Panel2;
   TLabel *Label10;
   TEdit *Edit2;
   TLabel *Label11;
   TEdit *Edit3;
   TUpDown *UpDown2;
   TUpDown *UpDown3;
   TSaveDialog *SaveDialog1;
   TLabel *Label12;
   TButton *Button2;
   TLabel *Label13;
   TLabel *Label14;
   TProgressBar *ProgressBar1;
   TMemo *Memo1;
   TImage *Image1;
   void __fastcall FormResize(TObject *Sender);
   void __fastcall Button1Click(TObject *Sender);
   void __fastcall Button2Click(TObject *Sender);
   void __fastcall Edit1KeyPress(TObject *Sender, char &Key);
   void __fastcall Button3Click(TObject *Sender);
private:	// User declarations
public:		// User declarations
    //Save
   BYTE DataSektor[4048];
   void  SaveSektorToFile(String FileName);
   //read
   void  DriveRead(void);

   __fastcall TForm1(TComponent* Owner);
};
//---------------------------------------------------------------------------
extern PACKAGE TForm1 *Form1;
//---------------------------------------------------------------------------
#endif
