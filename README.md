# Parking-managment-system
This C++ program implements a Parking Lot Management System using Doubly Linked Lists and Queues. It allows users to add, remove, search, and display vehicles, with a queue handling overflow when the lot is full. The system simulates real-world parking scenarios, ensuring efficient vehicle management. Ideal for learning data structures in C++.



#include <iostream>
using namespace std;

class Vehicle 
{
private:
    string platenumber;
    string vehicletype;
    Vehicle* next;
    Vehicle* previous;
    
public:
    //constructer
    Vehicle(string platenumber, string vehicletype)
    {
        this->platenumber = platenumber;
        this->vehicletype = vehicletype;
        this->next = NULL;
        this->previous = NULL;
    }
    //getter\setter
    string getPlatenumber()
    {
        return platenumber;
    }
    void setPlatenumber(string platenumber)
    {
        this->platenumber = platenumber;
    }
    string getVehicletype()
    {
        return vehicletype;
    }
    void setVehicle(string vehicletype)
    {
        this->vehicletype = vehicletype;
    }
    Vehicle* getNext()
    {
        return next;
    }
    void setNext(Vehicle* next)
    {
        this->next = next;
    }
    Vehicle* getPrevious()
    {
        return previous;
    }
    void setPrevious(Vehicle* previous)
    {
        this->previous = previous;
    }
};
class parkinglot
{
private:

    Vehicle* head;
    Vehicle* tail;
    int capacity;
    int currentvehicle;
    
public:
    //constructer
    parkinglot(int capacity) 
    {
        this->capacity = capacity;
        this->currentvehicle = 0;
        this->head = NULL;
        this->tail = NULL;
    }
    //Add vehicle
    bool insertVehicle( )
    {
        if (currentvehicle >= capacity)
        {
            cout << "Parking lot is full Cannot be parked!!!" << endl;
            return false;
        }

        string platenumber;
        string vehicletype;

        cout << "enter vehicle plate number:";
        cin >> platenumber;

        cout << "enter vehicle type:";
        cin >> vehicletype;

            Vehicle* newvehicle = new Vehicle (platenumber, vehicletype);

            if (head = NULL)
            {
                head = newvehicle;
                tail = newvehicle;
            }

            else
            {
                tail->setNext(newvehicle);
                newvehicle->setPrevious(tail);
                tail = newvehicle;
            }
            currentvehicle++;
            cout << "Vehicle is parked!!!" << platenumber << endl;
            return true;
        
    }
    //remove 
    void deleteVehicle(string platenumber)
    {
        if (head == NULL)
        {
            cout << "no vehicle is available to remove" << endl;
           return;
        }
        string platenumber;
        cout << "enter plate number you want to remove";
        cin >> platenumber;

        Vehicle* target = head;
        while (target != NULL)
        {
            if (target->getPlatenumber() == platenumber)
            {
                break;
            }
            target = target->getNext();
        }
        if (target == NULL)
        {
            cout << "Not found" <<platenumber << endl;
            return; //platenumber not found
        }
        Vehicle* previous = target->getPrevious();
        Vehicle* next = target->getNext();
        if (target == head)
        {
            head = next;
            if (head != NULL)
            {
                head->setPrevious(NULL);
            }
        }
        else
        {
            previous->setNext(next);
        }
        if (target == tail)
        {
            tail = previous;
            if (tail != NULL)
            {
                tail->setNext(NULL);
            }
        }
        else
        {
            if (next != NULL)
            {
                next->setPrevious(previous);
            }
        }
        delete target;

        currentvehicle--;

        cout << "Vehicle removed: " << platenumber <<endl;
        return;
    }
    //display
    void displayVehicle()
    {
        Vehicle* temp = head;
        if (temp==NULL) {
            cout << "No vehicles parked." << endl;
            return;
        }
        while (temp != NULL)
        {
            cout << "Plate Number::" << temp->getPlatenumber() << endl;
            cout << "Vehicle Type::" << temp->getVehicletype() << endl;
            temp = temp->getNext();
        }
    }
    //search
    void searchVehicle(string platenumber)
    {
        string searchplate;
        cout << "Enter the plate number to search: ";
        cin >> searchplate;


        bool found = false;
        Vehicle* temp = head;
        while (temp != NULL)
        {
            if (temp->getPlatenumber() == platenumber)
            {
                found = true;
                break;
            }
            temp = temp->getNext();
        }
        if (found)
        {
            cout << "vehicle found::" << endl;
        }
        else
        {
            cout << "vehicle not found::" << endl;
        }
    }
    
};

class queue
{
private:
    Vehicle* front;
    Vehicle* rear;

public:
    queue()
    {
        this->front = NULL;
        this->rear = NULL;
    }
    bool empty() 
    {
        return front == NULL;
    }
    void enqueue(string platenumber, string vehicletype)
    {
        string paltenumber;
        string vehicletype;
        cout << "Enter vehicle plate number: ";
        cin >> platenumber;
        cout << "Enter vehicle type: ";
        cin >> vehicletype;

        Vehicle* newvehicle = new Vehicle(platenumber, vehicletype);
        if (empty()) 
        {
            front  = newvehicle;
            rear = newvehicle;
        }
        else
        {
            rear->setNext(newvehicle);
            rear = newvehicle;
        }
        cout << "Vehicle added to queue: " << platenumber << endl;
    }
    void dequeue(parkinglot& lot)
    {
        if (empty() )
        {
            cout << "Queue is empty!" << endl;
            return;
        }
        Vehicle* temp = front;
        //they can take vehicle detail
        lot.insertVehicle(); 
        temp = temp->getNext();
        if (front==NULL)
        {
            rear = NULL; 
        }
        delete temp;
    }
    void searchQueue(string platenumber) {
        string searchplate;
        cout << "Enter the plate number to search in queue: ";
        cin >> searchplate;


        bool found = false;
        Vehicle* temp = front;
        while (temp != NULL)
        {
            if (temp->getPlatenumber() == platenumber)
            {
                found = true;
                break;
            }
            temp = temp->getNext();
        }
        if (found)
        {
            cout << "vehicle found::" << endl;
        }
        else
        {
            cout << "vehicle not found::" << endl;
        }
    
    }

    void displayQueueVehicle(string platenumber) {
        Vehicle* temp = front;
        bool found = false;

        while (temp != NULL) {
            if (temp->getPlatenumber() == platenumber) {
                found = true;
                cout << "Vehicle found in queue:" << endl;;
                cout << "Plate Number: " << temp->getPlatenumber() << endl;
                cout << "Vehicle Type: " << temp->getVehicletype() << endl;
                break;
            }
            temp = temp->getNext();
        }

        if (!found) {
            cout << "Vehicle not found in queue."<<endl;
        }
    }
};


int main()
{
    parkinglot lot(3); //setting the capacity of 3 vehicle
    queue wqueue;

    int choice;

    do {
        cout << " :::  *Parking lot Managment System* :::  " << endl;
        cout << "Press 1 for Add vehicle in parking lot" << endl;
        cout << "Press 2 for remove vehicle from parking lot " << endl;
        cout << "Press 3 for display vehicle from parking lot" << endl;
        cout << "Press 4 for Add vehicle from Queue" << endl;
        cout << "Press 5 for Dequeue from Queue" << endl;
        cout << "Press 6 for search vehicle form (parking lot)" << endl;
        cout << "Press 7 for search vehicle form Dequeue" << endl;

        cout << "Press 8 for exit Managment system" << endl;
        cout << "Enter yor choice" << endl;
        cin >> choice;

        string platenumber;
        string searchplate;
        string queueSearchplate;

        switch (choice) {
        case 1:
            lot.insertVehicle();
            break;
        case 2:
            
            cout << "Enter the plate number of the vehicle to remove: ";
            cin >> platenumber;
            lot.deleteVehicle(platenumber);
            break;
        case 3:
            lot.displayVehicle();
            break;
        case 4:
            wqueue.enqueue("a","d");
            break;
        case 5:
            wqueue.dequeue(lot);
            break;
        case 6:
            
            cout << "Enter the plate number to search: ";
            cin >> searchplate;
            lot.searchVehicle(searchplate);
            break;
        case 7:
            
            cout << "Enter the plate number to search in the queue: ";
            cin >> queueSearchplate;
            wqueue.displayQueueVehicle(queueSearchplate);
            break;
        case 8:
            cout << "Existing.........." << endl;
            break;
        default:
            cout << "Invalid choice..please try again" << endl;
            
        }

    } while (choice != 8);



    return 0;
}
