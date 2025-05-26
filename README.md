# Spoofer-Hwid
Usado Pra tirar Ban de Jogos Como Mta , FiveM , Valorant Etc ( este codigo nao esta 100% funcional e somente uma base )

using System;
using System.Management;

class HWIDSpoofer
{
    static string spoofedHWID = null;
    
    static void Main()
    {
        while (true)
        {
            Console.Clear();
            Console.WriteLine("== HWID Spoofer By Muffyn==");
            Console.WriteLine("1. Ver HWID real");
            Console.WriteLine("2. Gerar HWID spoofado aleatório");
            Console.WriteLine("3. Definir HWID spoofado manualmente");
            Console.WriteLine("4. Ver HWID atual (real ou spoofado)");
            Console.WriteLine("5. Resetar spoof");
            Console.WriteLine("0. Sair");
            Console.Write("Escolha uma opção: ");
            string escolha = Console.ReadLine();

            switch (escolha)
            {
                case "1":
                    Console.WriteLine("\nHWID real: " + GetRealHWID());
                    break;
                case "2":
                    spoofedHWID = GenerateRandomHWID();
                    Console.WriteLine("\nHWID spoofado definido: " + spoofedHWID);
                    break;
                case "3":
                    Console.Write("\nDigite o HWID spoofado: ");
                    spoofedHWID = Console.ReadLine();
                    Console.WriteLine("HWID spoofado definido.");
                    break;
                case "4":
                    Console.WriteLine("\nHWID atual: " + GetCurrentHWID());
                    break;
                case "5":
                    spoofedHWID = null;
                    Console.WriteLine("\nSpoof removido. HWID real restaurado.");
                    break;
                case "0":
                    return;
                default:
                    Console.WriteLine("\nOpção inválida.");
                    break;
            }

            Console.WriteLine("\nPressione qualquer tecla para continuar...");
            Console.ReadKey();
        }
    }

    static string GetCurrentHWID()
    {
        return spoofedHWID ?? GetRealHWID();
    }

    static string GetRealHWID()
    {
        try
        {
            string hwid = "";
            ManagementObjectSearcher searcher = new ManagementObjectSearcher("SELECT * FROM Win32_ComputerSystemProduct");
            foreach (ManagementObject obj in searcher.Get())
            {
                hwid = obj["UUID"].ToString();
                break;
            }
            return hwid;
        }
        catch
        {
            return "Erro ao obter HWID real.";
        }
    }

    static string GenerateRandomHWID()
    {
        return Guid.NewGuid().ToString().ToUpper();
    }
}

