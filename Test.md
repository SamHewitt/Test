// Sam Hewitt
// Family Feud Assignment
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.IO;
using System.Threading;

namespace Family_Feud_Sam_Hewitt
{
    public struct Questions
    {

        public static string questions;
        public static string answers;
        public string accept;
        public static int points;

    }

    public struct Student
    {
        public string lastName;
        public string firstName;
        public string Interest;



    }
    class Program

    {

        public static void Main(string[] args)
        {

            Student[] info = new Student[43];
            string player = "";
            Load(info);
            Menu(info, ref player);
        }
        static void Menu(Student[] info, ref string player) // Menu for Family Feud
        {
            char task;
            // Do while
            do
            {
                Console.Clear();
                Console.BackgroundColor = ConsoleColor.DarkRed;
                Console.ForegroundColor = ConsoleColor.Cyan;

                Console.WriteLine(@"  
  ███████╗ █████╗ ███╗   ███╗██╗██╗  ██╗   ██╗    ███████╗███████╗██╗   ██╗██████╗
  ██╔════╝██╔══██╗████╗ ████║██║██║  ╚██╗ ██╔╝    ██╔════╝██╔════╝██║   ██║██╔══██╗
  █████╗  ███████║██╔████╔██║██║██║   ╚████╔╝     █████╗  █████╗  ██║   ██║██║  ██║
  ██╔══╝  ██╔══██║██║╚██╔╝██║██║██║    ╚██╔╝      ██╔══╝  ██╔══╝  ██║   ██║██║  ██║
  ██║     ██║  ██║██║ ╚═╝ ██║██║███████╗██║       ██║     ███████╗╚██████╔╝██████╔╝
  ╚═╝     ╚═╝  ╚═╝╚═╝     ╚═╝╚═╝╚══════╝╚═╝       ╚═╝     ╚══════╝ ╚═════╝ ╚═════╝ ");
                Console.WriteLine("=====================================================================================");
                Console.ForegroundColor = ConsoleColor.DarkRed;
                Console.WriteLine("                                     Sam Hewitt ");
                Console.ForegroundColor = ConsoleColor.Blue;
                Console.WriteLine(@"
                              _________________________
                             |                         |
                             |   1   Load              |
                             |   2   Display Names     |
                             |   3   Sort              |
                             |   4   Update Interest   |
                             |   5   Play              |
                             |   0   Exit              |
                             |                         |");
                Console.ForegroundColor = ConsoleColor.Cyan;
                Console.WriteLine("=====================================================================================");
                Console.ForegroundColor = ConsoleColor.Blue;
                task = Convert.ToChar(Console.ReadLine());
                Console.Clear();
                // Switch statements
                switch (task)
                {
                    case '0':
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("Exit Program");
                        Console.ReadLine();
                        break;
                    case '1':
                        Load(info);
                        Console.Clear();
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("Data loaded\nPress enter to continue");
                        Console.ReadLine();
                        break;
                    case '2':
                        Display(info);
                        Console.Clear();
                        break;
                    case '3':
                        Sort(info, ref player);
                        Console.Clear();
                        break;
                    case '4':
                        UpdateInterest(info, ref player);
                        break;
                    case '5':
                        Play(info, ref player);
                        // Play(info);
                        Console.Clear();
                        break;

                    default:
                        Console.WriteLine("Invalid Input");
                        Thread.Sleep(500);
                        Console.WriteLine("Press enter to continue");
                        Console.ReadLine();
                        break;
                }

            } while (task != '0');
        }
        static void Load(Student[] info)// Loads data from directory
        {
            StreamReader sr = new StreamReader($@"{Directory.GetCurrentDirectory()}\Familyfeud.txt");
            int count = 0;
            while (count < 43)
            {
                info[count].firstName = sr.ReadLine();
                info[count].lastName = sr.ReadLine();
                info[count].Interest = sr.ReadLine();
                count++;
            }
        }
        public static void Display(Student[] info)// Displays Contestant Info
        {
            Console.WriteLine("Contestant info");
            Console.WriteLine($"First Name".PadRight(18) + "Last Name".PadRight(18) + "Interest");
            for (int i = 0; i < info.Length; i++)
            {
                Console.WriteLine($"{info[i].firstName.PadRight(18)}|{info[i].lastName.PadRight(18)}|{info[i].Interest}");
            }
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine("Press enter to return to the Main Menu");
            Console.ForegroundColor = ConsoleColor.Blue;
            Console.ReadLine();
        }
        public static void Sort(Student[] info, ref string player)// Sorts the Contestants Alphabetically
        {

            char task;
            do
            {
                Console.WriteLine("1     Alphabetical order first name");
                Console.WriteLine("2     Alphabetical order last name");
                Console.WriteLine("3     Main Menu");
                task = Convert.ToChar(Console.ReadLine());
                Console.Clear();
                switch (task)
                {
                    case '1':

                        for (int i = 0; i < info.Length; i++)
                        {
                            for (int pos = 0; pos < info.Length - 1; pos++)
                            {
                                if (info[pos + 1].firstName.CompareTo(info[pos].firstName) < 0)
                                {
                                    Student temp;
                                    temp = info[pos + 1];
                                    info[pos + 1] = info[pos];
                                    info[pos] = temp;
                                }
                            }
                        }
                        Console.Clear();
                        Console.WriteLine("Contestant info");
                        Console.WriteLine($"First Name".PadRight(18) + "Last Name".PadRight(18) + "Interest".PadRight(18));
                        Console.Clear();
                        Display(info);
                        Console.WriteLine("Press enter to return to sorting menu");
                        Console.Clear();

                        break;
                    case '2':
                        for (int i = 0; i < info.Length; i++)
                        {
                            for (int pos = 0; pos < info.Length - 1; pos++)
                            {
                                if (info[pos + 1].lastName.CompareTo(info[pos].lastName) < 0)
                                {

                                    Student temp;
                                    temp = info[pos + 1];
                                    info[pos + 1] = info[pos];
                                    info[pos] = temp;

                                }
                            }
                        }
                        Console.WriteLine("Contestant info");
                        Console.WriteLine($"First Name".PadRight(18) + "Last Name".PadRight(18) + "Interest".PadRight(18));
                        for (int i = 0; i < info.Length; i++)
                        {
                            Console.WriteLine($"{info[i].firstName.PadRight(18)}|{info[i].lastName.PadRight(18)}|{info[i].Interest.PadRight(18)}");
                        }
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("Press enter to return to sorting menu");
                        Console.ReadLine();
                        Console.Clear();
                        Console.ForegroundColor = ConsoleColor.Blue;
                        Sort(info, ref player);
                        break;
                    case '3':
                        Menu(info, ref player);
                        break;
                    default:
                        Menu(info, ref player);
                        break;
                }
            } while (task != '0');
        }

        public static void UpdateInterest(Student[] info, ref string player)// Update the Interest of Contestants
        {

            {
                Console.Clear();
                Console.WriteLine("Would you like to update a contestant's interest?(Y/N)");
                string choiceyes = Console.ReadLine();
                if (choiceyes == "Y" || choiceyes == "Yes" || choiceyes == "y" || choiceyes == "yes")
                {
                    Console.Clear();
                    Console.WriteLine("Which Contestants info would you like to update?");
                }
                else if (choiceyes == "N" || choiceyes == "No" || choiceyes == "n" || choiceyes == "no")
                {
                    Menu(info, ref player);
                }

                else
                {
                    Console.ForegroundColor = ConsoleColor.Green;
                    Console.WriteLine("Invalid Input, try again");
                    Console.ReadLine();
                    Console.ForegroundColor = ConsoleColor.Blue;
                    UpdateInterest(info, ref player);
                }
                string wanted = Console.ReadLine();
                for (int i = 0; i < info.Length; i++)
                {
                    if (info[i].firstName == wanted)
                    {
                        Console.WriteLine($"Contestant:{info[i].firstName} {info[i].lastName}\nInterest:{info[i].Interest}");
                        Console.Clear();
                        Console.WriteLine($"Would you like to change {info[i].firstName} {info[i].lastName}'s interest?(Y/N)");
                        Console.ForegroundColor = ConsoleColor.Green;
                        Console.WriteLine("Press enter to return");
                        Console.ForegroundColor = ConsoleColor.Blue;
                        string choice = Console.ReadLine();
                        if (choice == "Y" || choice == "Yes" || choice == "y" || choice == "yes")
                        {
                            Console.Clear();
                            Console.WriteLine("What would you like to change their interest to?");
                            info[i].Interest = Console.ReadLine();
                        }
                        else if (choice == "N" || choice == "No" || choice == "n" || choice == "no")
                        {
                            UpdateInterest(info, ref player);
                        }
                    }
                }

            }
        }
        public static void GenerateFinalists(Student[] info, ref string player)// Randomly generate 10 game finalists
        {
            int num = 0;
            Console.WriteLine("Its time to generate 10 finalists for Family Feud!\nThe lucky finalists are");
            Random rand = new Random();
            Student[] Finalists = new Student[10];
            for (int i = 0; i < Finalists.Length; i++)
            {
                num = rand.Next(0, info.Length);
                while (Finalists.Contains(info[num]))
                {
                    num = rand.Next(0, info.Length);
                }
                Finalists[i] = info[num];
            }
            for (int i = 0; i < Finalists.Length; i++)
            {
                Console.ForegroundColor = ConsoleColor.Green;
                Console.WriteLine($"{Finalists[i].firstName} {Finalists[i].lastName}");
                Console.ForegroundColor = ConsoleColor.Blue;
            }

            Console.ReadLine();
            Console.Clear();
            Console.WriteLine("Our first player is"); // Randomly generate one player from the finalists
            Random rand2 = new Random();
            num = rand2.Next(0, 10);
            player = $"{Finalists[num].firstName} {Finalists[num].lastName}";

            Student[] Finalist = new Student[1];
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine(player);
            Console.ForegroundColor = ConsoleColor.Blue;
            for (int i = 0; i < Finalist.Length; i++)
            {
                Console.ForegroundColor = ConsoleColor.Green;
                Console.WriteLine($"{Finalist[i].firstName} {Finalist[i].lastName}");
                Console.ForegroundColor = ConsoleColor.Blue;
            }
            Console.ReadLine();
            Console.Clear();

        }


        public static void Intro(Student[] info, ref string player)// Introduces game, asks if want to update interest
        {
            string interest = " ";
            Console.ForegroundColor = ConsoleColor.Green;
            Console.WriteLine(player);
            Console.ForegroundColor = ConsoleColor.Blue;
            Console.WriteLine("Are you ready to play Family Feud?(Y/N)");
            string choice1 = Console.ReadLine();
            if (choice1 == "Y" || choice1 == "Yes" || choice1 == "y" || choice1 == "yes")
            {
                Console.Clear();
                string[] temp = player.Split(' ');
                for (int i = 0; i < info.Length; i++)
                {
                    if (info[i].firstName == temp[0])
                    {
                        Console.WriteLine($"Would you like to change {player}'s interest?(Y/N)");
                        Console.ForegroundColor = ConsoleColor.Blue;
                        string choice = Console.ReadLine();
                        if (choice == "Y" || choice == "Yes" || choice == "y" || choice == "yes")
                        {
                            Console.Clear();
                            Console.WriteLine("What would you like to change their interest to?");
                            info[i].Interest = Console.ReadLine();
                            interest = $"{info[i].Interest}";

                        }
                        else if (choice == "N" || choice == "No" || choice == "n" || choice == "no")
                        {

                        }
                    }
                }
            }
            else if (choice1 == "N" || choice1 == "No" || choice1 == "n" || choice1 == "no")
            {

            }
            if (interest.Length <= 1)
            {
                Console.WriteLine($"{player}, heres your first question:");
                Console.ReadLine();
            }
            else
            {
                Console.WriteLine($"{player} you enjoy {interest}, thats sounds like fun\nHeres your first question:");
                Console.ReadLine();
            }


        }
        public static void Play(Student[] info, ref string player)// Play Family Feud
        {

            GenerateFinalists(info, ref player);
            Intro(info, ref player);
            LoadQuestions();
            int attempts = 0;
            bool no = false;
            bool correct = false;
            for (int i = 0; i < 2; i++)
            {
                no = false;
                attempts = 0;
                do
                {
                    no = true;
                    correct = false;
                    Console.WriteLine([i]);
                string answer = Console.ReadLine();
            }
        }
    }
    public static void LoadQuestions()
    {

        Questions[] Question = new Questions[3];
        StreamReader sr = new StreamReader("FamilyFeudQs.txt");
        for (int i = 0; i < Question.Length; i++)

        {
            LoadQuestions[i].questions = sr.ReadLine();
            LoadQuestions[i].answer = sr.ReadLine().Split(',');
            LoadQuestions[i].points = sr.ReadLine().Split(',');


        }
        sr.Close();
    }
}
