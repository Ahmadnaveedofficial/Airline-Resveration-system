#include <iostream>
#include <fstream>
#include <string>
#include <iomanip>

using namespace std;

struct Flight
 {
    string flightNumber;
    string destination;
    string departureTime;
    string duration;
    float price;
};

struct Customer 
{
    int customerId;
    string name;
    int age;
    string gender;
    string address;
    string phone;
};

void inputCustomerDetails(Customer& customer) 
{
    cout << "Enter Customer ID: ";
    cin >> customer.customerId;
    cin.ignore();
    cout << "Enter Name: ";
    getline(cin, customer.name);
    cout << "Enter Age: ";
    cin >> customer.age;
    cin.ignore();
    cout << "Enter Gender: ";
    getline(cin, customer.gender);
    cout << "Enter Address: ";
    getline(cin, customer.address);
    cout << "Enter Phone Number: ";
    getline(cin, customer.phone);
    cout << "Customer details saved successfully!" << endl;
}

void displayFlights(const Flight flights[], int flightCount) 
{
    cout << left << setw(10) << "Flight No" << setw(15) << "  Destination"
        << setw(20) << "   Departure" << setw(10) << "Duration\t" 
        << "Price" << endl;
    for (int i = 0; i < flightCount; ++i)
	 {
        cout << left << setw(10) << flights[i].flightNumber
            << setw(15) << flights[i].destination
            << setw(20) << flights[i].departureTime
             << flights[i].duration << setw(10)<< " hours"
            << "Rs." << flights[i].price << endl;
    }
}

void printTicket(int ticketId, const Customer& customer, const Flight& flight) 
{
    ofstream outf("ticket.txt");
    if (outf.is_open())
	 {
        outf << "************* Airline Ticket *************\n";
        outf << "Ticket ID: " << ticketId << endl;
        outf << "Customer Name: " << customer.name << endl;
        outf << "Customer Gender: " << customer.gender << endl;
        outf << "Flight Number: " << flight.flightNumber << endl;
        outf << "Destination: " << flight.destination << endl;
        outf << "Departure Time: " << flight.departureTime << endl;
        outf << "Duration: " << flight.duration << " hours" << endl;
        outf << "Price: Rs. " << flight.price << endl;
    }
    outf.close();
    cout << "Ticket has been printed! Check 'ticket.txt'.\n";
}

void displayTicket(int ticketId, const Customer& customer, const Flight& flight) 
{
    cout << "************* Airline Ticket *************\n";
    cout << "Ticket ID: "        << ticketId << endl;
    cout << "Customer Name: "    << customer.name << endl;
    cout << "Customer Gender: "  << customer.gender << endl;
    cout << "Flight Number: "    << flight.flightNumber << endl;
    cout << "Destination: "      << flight.destination << endl;
    cout << "Departure Time: "   << flight.departureTime << endl;
    cout << "Duration: "         << flight.duration << " hours" << endl;
    cout << "Price: Rs. "        << flight.price << endl;
}

void getFlights(Flight flights[], int& flightCount)
 {
    flights[0] = { "DUB-498", "   Dubai",     "08-12-2024 7:40PM", "04",  14000 };
    flights[1] = { "CA-198",  "   Canada",    "22-01-2024 5:40AM", "16", 34000 };
    flights[2] = { "UK-798",  "   UK",        "09-12-2024 7:40PM", "14", 44000 };
    flights[3] = { "US-578",  "   USA",       "25-02-2024 5:40AM", "18", 94000 };
    flights[4] = { "AS-898",  "   Australia", "22-01-2024 5:40AM", "16", 64000 };
    flights[5] = { "EU-348",  "   Europe",    "22-01-2024 5:40AM", "07",  78000 };
    flightCount = 6;
}

void mainMenu()
 {
    int choice, ticketId = 8989;
    Customer customer;
    Flight flights[10];
    int flightCount = 0;
    getFlights(flights, flightCount);
    Flight selectedFlight;
    bool flightBooked = false;

    while (true) {
        cout << "\t                 XYZ Airlines \n" << endl;
        cout << "\t__Main Menu" << endl;
        cout << "\t _____________________________________________" << endl;
        cout << "\t |\t\t\t\t\t      |" << endl;
        cout << "\t |\t 1. Add Customer Details              |" << endl;
        cout << "\t |\t 2. View Available Flights            |" << endl;
        cout << "\t |\t 3. Book a Flight                     |" << endl;
        cout << "\t |\t 4. Print Ticket                      |" << endl;
        cout << "\t |\t 5. Exit                              |" << endl;
        cout << "\t |\t\t\t\t\t      |" << endl;
        cout << "\t _____________________________________________" << endl;
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) 
		{
        case 1:
            cout << "Enter Customer Details:\n";
            inputCustomerDetails(customer);
            break;
        case 2:
            cout << "\nAvailable Flights:\n";
            displayFlights(flights, flightCount);
            break;
        case 3:
		 {
            cout << "Select a flight by entering the flight number: ";
            string selectedFlightNumber;
            cin >> selectedFlightNumber;

            bool flightFound = false;
            for (int i = 0; i < flightCount; ++i) 
			{
                if (flights[i].flightNumber == selectedFlightNumber) 
				{
                    selectedFlight = flights[i];
                    flightFound = true;
                    flightBooked = true;
                    break;
                }
            }

            if (flightFound) 
			{
                cout << "Flight booked successfully!\n";
                displayTicket(ticketId++, customer, selectedFlight);
            }
            else 
			{
                cout << "Invalid flight number! Please try again.\n";
            }
            break;
        }
        case 4:
            if (flightBooked)
			 {
                printTicket(ticketId-1, customer, selectedFlight);
            }
            else 
			{
                cout << "No ticket has been booked yet.\n";
            }
            break;
        case 5:
            cout << "Thank you for using XYZ Airlines!\n";
            return;
        default:
            cout << "Invalid choice! Please try again.\n";
        }
    }
}

int main()
 {
 	  // Change background to green and text to black
    system("color 3F"); // Format: "color BG", where B = Background, G = Text
    
    cout << "The background is green, and the text is black!" << endl;

    mainMenu();
   

  
    return 0;
}
