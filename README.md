using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Diagnostics;

namespace ConsoleApplication1
{
    class Program
    {

        static void Main(string[] args)
        {
            int[] dizi = new int[10000];
            Random rnd = new Random();
            int sayi;
            for (int i = 0; i < 10000; i++)
            {
            to:
                sayi = rnd.Next(-10000, 10000);
                if (dizi.Contains(sayi) != true)
                {
                    dizi[i] = sayi;
                }
                else
                {
                    goto to;
                }
            }
            Console.WriteLine("{0} değerli bir dizi için;", dizi.Length);
            //kabarcik(dizi);
            secsiralama(dizi);
            Console.ReadKey();
        }
        public static void kabarcik(int[] dizi)
        {
            Stopwatch sayac = new Stopwatch();
            sayac.Start();
            int i = 1, j, bosdeger,islemadet=0,yerdegistirme=0;
            int diziAdet = dizi.Length;
            while (i < diziAdet) // n olan dizi adeti 1 den küçükse işlemi yap
            {
                j = diziAdet - 1; // diziadet-1 sonucunu j ye aktar
                while (j >= 1) //j deki değer 1den büyük veya eşitse işleme gir
                {
                    if (dizi[j - 1] > dizi[j]) // dizi[j-1] değeri dizi[j] den büyükse işlemi yap örn: dizi[99-1] > dizi[99](dizi[99] un içinde 1 dizi[99-1]in içinde 2 var ise)
                    {
                        yerdegistirme++; // yer değiştirme olayı olduğu için yer değiştirme adetini arttır
                        islemadet++; // işlem için adet arttır
                        bosdeger = dizi[j]; // dizi[99] değerini yani 1 değerini boş değerin içine at (örnek)
                        dizi[j] = dizi[j - 1]; // dizi[99] kopyası olduğu için dizi[99]un içine dizi[98] i yani 2 değerini at (örnek)
                        dizi[j - 1] = bosdeger; // kopyaladığımız değeri dizi[98]e at bu durumda 1 değerini kopyalayıpı 2 değerini 1in üzerine kopyaladığımız değeri 2nin olduğu indexe attık.
                    }
                    j--; // bir önceki index için kontrol
                }
                i++; // sıradaki değer
            }
            sayac.Stop();
            Console.WriteLine("(Baloncuk Algoritması)\nSüre:{0} milisaniye sürmüştür.\nİşlem Adeti: {1}\nYer değiştirme adeti: {2}", sayac.Elapsed.Milliseconds, islemadet, yerdegistirme);

        }

        public static void secsiralama(int[] dizi)
        {

            Stopwatch sayac = new Stopwatch();
            sayac.Start();
            int enkucuk, yedek, islemadet = 0, yerdegistirme = 0 ;
            for (int i = 0; i < dizi.Length - 1; i++)
            {
                enkucuk = i;
                for (int j = i + 1; j < dizi.Length; j++)
                {
                    if (dizi[j] < dizi[enkucuk])
                    {
                        islemadet++;
                        enkucuk = j;
                    }
                }

                if (enkucuk != i) 
                {
                    islemadet++;
                    yerdegistirme++;
                    yedek = dizi[i]; 
                    dizi[i] = dizi[enkucuk]; 
                    dizi[enkucuk] = yedek;
                }
            }
            Console.WriteLine("(Seçmeli sıralama algoritması)\nSüre:{0} milisaniye sürmüştür.\nİşlem adeti: {1}\nYer değiştirme adeti: {2}", sayac.Elapsed.Milliseconds, islemadet, yerdegistirme); //Geçen süreyi işlem adetini ekrana yazıyor.
        }
    }
}
