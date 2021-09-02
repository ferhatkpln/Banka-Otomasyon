#include <stdio.h>
#include <conio.h>
#include <Windows.h>
#include <stdlib.h>
#include <locale.h>
#include <time.h>
struct MusteriMenu
{
    char Kullanici_Adi[20];//ana menude kullanici adini almak icin...
    char Parola[20];//ana menude kullanici parola almak icin...
}mmenu;
struct musteri{//musteri ekleme de veya hesap acmadan kullaniliyor...
    char *ad;
    char *soyad;
    int tcno[11];
    int *musterino;
    int telno[11];
}ms;
enum Secim{
    Giris_Yap=1,
    Hesap_Ac,

};
    FILE *TKullaniciF;
    FILE *BKullaniciF;
int main()
{
    enum Secim secim;
    printf("***************************************\n");
    printf("**************HOSGELDINIZ**************\n\n");
    printf("NE YAPMAK ISTEDIGINIZ SECINIZ::");
    printf("\nGIRIS YAPMAK ICIN-1::");
    printf("\nHESAP ACMAK ICIN-2::\n");
    printf("Seciminiz::");
    scanf("%d",&secim);
    if(secim==Giris_Yap)
    {
       Giris();
       Baska_Islem();
    }
    else if(secim==Hesap_Ac)
    {
        YeniHesapAc();
        Baska_Islem();
    }
    else
        printf("HATALI SECIM YAPTINIZ!!!\n");
    main();
}

void Giris()
{
        system("CLS");
        printf("*********************************\n");
        printf("**************GIRIS**************\n");
        printf("Lutfen Musteri Tipini Seciniz::");
        printf("\nTicari Musteri Icin   -1::");
        printf("\nBireysel Musteri Icin -2::\n");
        printf("Seciminiz::");
        int mtip;
        scanf("%d",&mtip);
        if(mtip==1)
        {

            printf("Lutfen Kullanici Adinizi Giriniz::");
            scanf("%s",&mmenu.Kullanici_Adi);
            printf("Lutfen Parolanizi Giriniz::");
            scanf("%s",&mmenu.Parola);
            int sonuc1=2;
            int sonuc2=2;
            sonuc1=strcmp(mmenu.Kullanici_Adi,"ticarim");
            sonuc2=strcasecmp(mmenu.Parola,"55555");
            if(sonuc1==0 && sonuc2==0)
            {
                Menu2();
            }
            else
            {
                printf("Kullanici Adi veya Parola Hatali!!\n");
                Sleep(2000);
                Giris();
            }
        }
        else if(mtip==2)
        {
            printf("Lutfen Kullanici Adinizi Giriniz::");
            scanf("%s",&mmenu.Kullanici_Adi);
            printf("Lutfen Parolanizi Giriniz::");
            scanf("%s",&mmenu.Parola);
            int sonuc1=2;
            int sonuc2=2;
            sonuc1=strcmp(mmenu.Kullanici_Adi,"bireyselm");
            sonuc2=strcasecmp(mmenu.Parola,"666666");
            if(sonuc1==0 && sonuc2==0)
            {
                Menu2();
            }
            else
            {
                printf("Kullanici Adi veya Parola Hatali!!\n");
                Sleep(2000);
                Giris();
            }
        }
        else
        {
            printf("HATALI SECIM YAPTINIZ!!!\n");
            Giris();
        }
        Baska_Islem();
}
void Menu2()
{
    system("CLS");
    printf("***************************************\n");
    printf("**************ANA MENU**************\n\n\n");
    printf("Yapmak Istediginiz Islemi Seciniz\n");
    printf("\t1-Yeni Musteri Ekle\n");
    printf("\t2-Hesap Kapatma\n\n\n");
    printf("**************************************\n");
    printf("**************************************\n");
    int islem;
    printf("Yapmak Istediginiz Islem:");
    scanf("%d",&islem);
    if(islem==1)
    {
        Musteri_Ekle();
    }
    else if(islem==2)
    {
        Hesap_Kapatma();
    }
    else
    {
        printf("\nHatali Secim Yaptiniz!!!");
        Menu2();
    }
}
void YeniHesapAc()
{
    system("CLS");
    printf("**************************************\n");
    printf("**************HESAP ACMA**************\n");
    printf("Lutfen Musteri Tipini Seciniz::");
    printf("\nTicari Musteri Icin   -1::");
    printf("\nBireysel Musteri Icin -2::\n");
    printf("Seciminiz::");
    int mtip;
    scanf("%d",&mtip);
    if(mtip==1)
    {
        if ((TKullaniciF = fopen ("TicariMusteri_Liste.txt", "a+")) == NULL)
        {
            printf("Dosya acma hatasi!");
            exit(1);
        }
        ms.ad = (char*)malloc(sizeof(char)*100);
        printf("Adinizi Giriniz:");
        scanf("%s",ms.ad);
        ms.soyad = (char*)malloc(sizeof(char)*100);
        printf("Soyadinizi Giriniz:");
        scanf("%s",ms.soyad);
        printf("Tc Numaranizi Giriniz:");
        scanf("%s",&ms.tcno);
        printf("Telefon Numaranizi Giriniz:");
        scanf("%s",&ms.telno);
        ms.musterino=(int*)malloc(sizeof(int)*100);
        int rastgele;
        srand(time(NULL));
        rastgele=1000+rand()%2000;
        ms.musterino=rastgele;
        fprintf(TKullaniciF,"%s\t\t%s\t\t%s\t%s\t%d\n",ms.ad,ms.soyad,ms.telno,ms.tcno,ms.musterino);
        fclose(TKullaniciF);
        Baska_Islem();
    }
    else if(mtip==2)
    {
        if ((BKullaniciF = fopen ("BireyselMusteri_Liste.txt", "a+")) == NULL)
        {
            printf("Dosya acma hatasi!");
            exit(1);
        }
        ms.ad = (char*)malloc(sizeof(char)*100);
        printf("Adinizi Giriniz:");
        scanf("%s",ms.ad);
        ms.soyad = (char*)malloc(sizeof(char)*100);
        printf("Soyadinizi Giriniz:");
        scanf("%s",ms.soyad);
        printf("Tc Numaranizi Giriniz:");
        scanf("%s",&ms.tcno);
        printf("Telefon Numaranizi Giriniz:");
        scanf("%s",&ms.telno);
        ms.musterino=(int*)malloc(sizeof(int)*100);
        int rastgele;
        srand(time(NULL));
        rastgele=2000+rand()%3000;
        ms.musterino=rastgele;
        fprintf(BKullaniciF,"%s\t\t%s\t\t%s\t%s\t%d\n",ms.ad,ms.soyad,ms.telno,ms.tcno,ms.musterino);
        fclose(BKullaniciF);
        Baska_Islem();
    }
    else
    {
        printf("HATALI SECIM YAPTINIZ!!!\n");
        YeniHesapAc();
    }
}
void Baska_Islem()
{
    char b_islem;
    printf("BASKA BIR ISLEM YAPMAK ISTIYORMUSUNUZ(E-e/H-h) ??");
    scanf("%s",&b_islem);
    if(b_islem == 'E' || b_islem == 'e')
    {
        system("CLS");
        main();
    }
    else
    {
        system("CLS");
        printf("GULE GULE...");
    }
        exit(1);
}
void Musteri_Ekle()
{
    system("CLS");
    printf("******************************************\n");
    printf("**************MUSTERI EKLEME**************\n");
    printf("Lutfen Musteri Tipini Seciniz::");
    printf("\nTicari Musteri Icin   -1::");
    printf("\nBireysel Musteri Icin -2::\n");
    printf("Seciminiz::");
    int mtip;
    scanf("%d",&mtip);
    if(mtip==1)
    {
        if ((TKullaniciF = fopen ("TicariMusteri_Liste.txt", "a+")) == NULL)
        {
            printf("Dosya acma hatasi!");
            exit(1);
        }
        ms.ad = (char*)malloc(sizeof(char)*100);
        printf("Adinizi Giriniz:");
        scanf("%s",ms.ad);
        ms.soyad = (char*)malloc(sizeof(char)*100);
        printf("Soyadinizi Giriniz:");
        scanf("%s",ms.soyad);
        printf("Tc Numaranizi Giriniz:");
        scanf("%s",&ms.tcno);
        printf("Telefon Numaranizi Giriniz:");
        scanf("%s",&ms.telno);
        ms.musterino=(int*)malloc(sizeof(int)*100);
        int rastgele;
        srand(time(NULL));
        rastgele=1000+rand()%2000;
        ms.musterino=rastgele;
        fprintf(TKullaniciF,"%s\t\t%s\t\t%s\t%s\t%d\n",ms.ad,ms.soyad,ms.telno,ms.tcno,ms.musterino);
        fclose(TKullaniciF);
        Baska_Islem();
    }
    else if(mtip==2)
    {
        if ((BKullaniciF = fopen ("BireyselMusteri_Liste.txt", "a+")) == NULL)
        {
            printf("Dosya acma hatasi!");
            exit(1);
        }
        ms.ad = (char*)malloc(sizeof(char)*100);
        printf("Adinizi Giriniz:");
        scanf("%s",ms.ad);
        ms.soyad = (char*)malloc(sizeof(char)*100);
        printf("Soyadinizi Giriniz:");
        scanf("%s",ms.soyad);
        printf("Tc Numaranizi Giriniz:");
        scanf("%s",&ms.tcno);
        printf("Telefon Numaranizi Giriniz:");
        scanf("%s",&ms.telno);
        ms.musterino=(int*)malloc(sizeof(int)*100);
        int rastgele;
        srand(time(NULL));
        rastgele=2000+rand()%3000;
        ms.musterino=rastgele;
        fprintf(BKullaniciF,"%s\t\t%s\t\t%s\t%s\t%d\n",ms.ad,ms.soyad,ms.telno,ms.tcno,ms.musterino);
        fclose(BKullaniciF);
        Baska_Islem();
    }
    else
    {
        printf("HATALI SECIM YAPTINIZ!!!\n");
        YeniHesapAc();
    }

}
void Hesap_Kapatma()
{
    FILE *Tmusteri1;
    FILE *Bmusteri1;
    system("CLS");
    printf("******************************************\n");
    printf("**************MUSTERI SILME***************\n");
    printf("Lutfen Musteri Tipini Seciniz::");
    printf("\nTicari Musteri Icin   -1::");
    printf("\nBireysel Musteri Icin -2::\n");
    int s_tip;
    scanf("%d",&s_tip);
    if(s_tip == 1)
    {
        char ch;
        int s_satir;
        int temp=1;
         if ((TKullaniciF = fopen ("TicariMusteri_Liste.txt", "r+")) != NULL)
         {
             ch=fgetc(TKullaniciF);
             while(ch!=EOF)
             {
                 printf("%c",ch);
                 ch=fgetc(TKullaniciF);
             }
             rewind(TKullaniciF);
             printf("\nSilmek Istediginiz Satir Numarasini Giriniz ::");
             scanf("%d",&s_satir);
             Tmusteri1=fopen("TicariMusteri_Liste1.txt","w");
             ch=fgetc(TKullaniciF);
             while(ch != EOF)
             {
                ch = fgetc(TKullaniciF);
                if (ch == '\n')
                    temp++;
                    if (temp != s_satir)
                    {

                        putc(ch, Tmusteri1);
                    }
             }
             fclose(Tmusteri1);
             fclose(TKullaniciF);
             remove("TicariMusteri_Liste.txt");
             rename("TicariMusteri_Liste1.txt","TicariMusteri_Liste.txt");
             TKullaniciF=fopen("TicariMusteri_Liste.txt","r");
             ch=fgetc(TKullaniciF);
             while(ch!=EOF)
             {
                 printf("%c",ch);
                 ch=fgetc(TKullaniciF);
             }
             fclose(TKullaniciF);
         }
         else
         {
             printf("Dosya Okuma Hatasi!!!");
             Hesap_Kapatma();
         }

    }
    else if(s_tip == 2)
    {
        char ch;
        int s_satir;
        int temp=1;
         if ((BKullaniciF = fopen ("BireyselMusteri_liste.txt", "r")) != NULL)
         {
             ch=fgetc(BKullaniciF);
             while(ch!=EOF)
             {
                 printf("%c",ch);
                 ch=fgetc(BKullaniciF);
             }
             rewind(BKullaniciF);
             printf("\nSilmek Istediginiz Satir Numarasini Giriniz ::");
             scanf("%d",&s_satir);
             Bmusteri1=fopen("BireyselMusteri_Liste1.txt","w");
             ch=fgetc(BKullaniciF);
             while(ch != EOF)
             {
                ch = fgetc(BKullaniciF);
                if (ch == '\n')
                    temp++;
                    if (temp != s_satir)
                    {

                        putc(ch, Bmusteri1);
                    }
             }
             fclose(Bmusteri1);
             fclose(BKullaniciF);
             remove("BireyselMusteri_Liste.txt");
             rename("BireyselMusteri_Liste1.txt","BireyselMusteri_Liste.txt");
             BKullaniciF=fopen("BireyselMusteri_Liste.txt","r");
             ch=fgetc(BKullaniciF);
             while(ch!=EOF)
             {
                 printf("%c",ch);
                 ch=fgetc(BKullaniciF);
             }
             fclose(BKullaniciF);
         }
         else
         {
             printf("Dosya Okuma Hatasi!!!");
             Hesap_Kapatma();
         }
    }
    else
    {
        printf("Musteri Tipini Dogru Seciniz!!!\n");
        Hesap_Kapatma();
    }
    Baska_Islem();
}

















