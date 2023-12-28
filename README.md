# public
Projet d'application de Réservations Des BUS.E-BUS

username :user
password: pass


#include <stdlib.h>
#include <string.h>
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include<conio.h>
#define MAX_BUSES 10
#define MAX_SEATS 32
#define MAX_TRAVELERS 50

struct Reservation {
    char travelerName[30];
    int busIndex;
    int seatNumber;
};

struct Bus {
    char busNumber[5];
    char driverName[20];
    int seats[MAX_SEATS];
};

struct Traveler {
    char username[20];
    char password[20];
};

void initBus(struct Bus *bus, const char *busNumber, const char *driverName) {
    strcpy(bus->busNumber, busNumber);
    strcpy(bus->driverName, driverName);

    for (int i = 0; i < MAX_SEATS; ++i) {
        bus->seats[i] = 0; 
    }
}

void initTraveler(struct Traveler *traveler, const char *username, const char *password) {
    strcpy(traveler->username, username);
    strcpy(traveler->password, password);
}
void login() {
    int a = 0, i = 0;
    char uname[10], c = ' ';
    char pword[10], code[10];
    char user[10] = "user";
    char pass[10] = "pass";
    do {
        system("cls");
        printf("\n\n   \xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\n");
        printf("\t    E.BUS RESERVATION");
        printf("\n   \xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd  LOGIN FORM  \xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd  ");
        printf("\n\n   ENTREZ VOTRE NOM: ");
        scanf("%s", uname);
        printf(" \n   ENTREZ PASSWORD: ");
        while (i < 10) {
            pword[i] = getch();
            c = pword[i];
            if (c == 13)
                break;
            else
                printf("*");
            i++;
        }
        pword[i] = '\0';

        i = 0;

        if (strcmp(uname, "user") == 0 && strcmp(pword, "pass") == 0) {
            printf("\n   \xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd");
            printf("  \n\n   BIENVENUE USER !!!!");
            printf("\n\n\n   Press any key to continue...");
            getch();
            break;
        } else {
            printf("\n   \xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd\xcd");
            printf("\n\n   LOGIN IS UNSUCESSFUL...PLEASE TRY AGAIN...");
            a++;

            getch();
        }
    } while (a <= 2);
    if (a > 2) {
        printf("\nSorry you have entered the wrong username and password for four times!!!");

        getch();
    }
    system("cls");
}
void displayMenu() {
   
   
   printf("\t\t\tBus Reservation System Project in C\n\n");
    printf("                        1. Creer un compte voyageur\n\t\t\t");
    printf("2. Creer une nouvelle reservation\n\t\t\t");
    printf("3. Afficher les details des bus\n\t\t\t");
    printf("4. Afficher et modifier les details d'une reservation\n\t\t\t" );
    printf("5. Afficher la liste des voyageurs\n\t\t\t");
    printf("6. Quitter\n\t\t\t");
}

void createTraveler(struct Traveler *travelers, int *numTravelers) {
    if (*numTravelers < MAX_TRAVELERS) {
        printf("Entrez le nom d'utilisateur: ");
        scanf("%s", travelers[*numTravelers].username);
        printf("Entrez le mot de passe : ");
        scanf("%s", travelers[*numTravelers].password);
        (*numTravelers)++;
        printf("Compte voyageur créé avec succès.\n");
    } else {
        printf("Limite de voyageurs atteinte. Impossible de créer un nouveau compte.\n");
    }
}

void createReservation(struct Reservation *reservations, int *numReservations, const struct Bus *buses, int numBuses) {
    if (*numReservations < MAX_SEATS * MAX_BUSES) {
        int busIndex, seatNumber;

        printf("Sélectionnez le bus (1----%d): ", numBuses);
        scanf("%d", &busIndex);

        if (busIndex < 1 || busIndex > numBuses) {
            printf("Bus invalide. Veuillez sélectionner un bus valide.\n");
            return;
        }

        printf("Sélectionnez la palce (1----%d): ", MAX_SEATS);
        scanf("%d", &seatNumber);

        if (seatNumber < 1 || seatNumber > MAX_SEATS) {
            printf("place invalide. Veuillez sélectionner une place valide.\n");
            return;
        }

        if (buses[busIndex - 1].seats[seatNumber - 1] == 0) {
            buses[busIndex - 1].seats[seatNumber - 1] == 1; 
            strcpy(reservations[*numReservations].travelerName, "N/A"); 
            reservations[*numReservations].busIndex = busIndex;
            reservations[*numReservations].seatNumber = seatNumber;
            (*numReservations)++;
            printf("Réservation créée avec succès.\n");
        } else {
            printf("La placee est déjà réservé. Veuillez selectionner une autre place.\n");
        }
    } else {
        printf("Limite de réservations atteinte. Impossible de créer une nouvelle réservation.\n");
    }
}

void displayBuses(const struct Bus *buses, int numBuses) {
    printf("\nDétails des bus :\n");
    for (int i = 0; i < numBuses; ++i) {
        printf("Bus %d - Numéro: %s, Conducteur: %s\n", i + 1, buses[i].busNumber, buses[i].driverName);
    }
}

void displayReservationDetails(const struct Reservation *reservations, int numReservations, const struct Bus *buses) {
    int reservationIndex;

    printf("Entrez le numéro de réservation (1-----%d): ", numReservations);
    scanf("%d", &reservationIndex);

    if (reservationIndex < 1 || reservationIndex > numReservations) {
        printf("Numéro de réservation invalide. Veuillez sélectionner un numéro valide.\n");
        return;
    }

    const struct Reservation *reservation = &reservations[reservationIndex - 1];
    const struct Bus *bus = &buses[reservation->busIndex - 1];

    printf("\nDétails de la reservation %d :\n", reservationIndex);
    printf("Nom du voyageur: %s\n", reservation->travelerName);
    printf("Bus: %s, Conducteur: %s\n", bus->busNumber, bus->driverName);
    printf("Siège: %d\n", reservation->seatNumber);

    int choice;
    printf("\n1. Modifier le nom du voyageur\n");
    printf("2. Retourner au menu principal\n");
    printf("Entrez votre choix: ");
    scanf("%d", &choice);

    if (choice == 1) {
        printf("Entrez le nouveau nom du voyageur: ");
        scanf("%s", reservation->travelerName);
        printf("Nom du voyageur modifie avec succes.\n");
    }
}

void displayTravelers(const struct Traveler *travelers, int numTravelers) {
    printf("\nListe des voyageurs :\n");
    for (int i = 0; i < numTravelers; ++i) {
        printf("Voyageur %d - Nom d'utilisateur: %s\n", i + 1, travelers[i].username);
    }
}

int main() {
    struct Bus buses[MAX_BUSES];
    struct Traveler travelers[MAX_TRAVELERS];
    struct Reservation reservations[MAX_SEATS * MAX_BUSES];
    int numBuses = 4; 
    int numTravelers = 0;
    int numReservations = 0;

   
    initBus(&buses[0], "TUNIEXPRESS", "SAMIR TOUNSI");
    initBus(&buses[1], "TTRAVEL", "AHMED");
    initBus(&buses[2], "TuneL", "MABROUK");
    initBus(&buses[3], "HIGHTUN", "SADDEM");
	int choice;

    do { 
	    login();
	    while (1) {
        printf("\nMenu principal :\n");
        displayMenu();

        printf("Entrez votre choix: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                createTraveler(travelers, &numTravelers);
                break;
            case 2:
                createReservation(reservations, &numReservations, buses, numBuses);
                break;
            case 3:
                displayBuses(buses, numBuses);
                break;
            case 4:
                displayReservationDetails(reservations, numReservations, buses);
                break;
            case 5:
                displayTravelers(travelers, numTravelers);
                break;
            case 6:
                printf("Merci d'avoir utilisé E-BUS. Au revoir!\n");
                break;
            default:
                printf("Choix invalide. Veuillez entrer un choix valide.\n");
        }
    }} while (choice != 6);

    return 0;
}



