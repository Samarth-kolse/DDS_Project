#include <iostream>
#include <string>
#include <vector>
#include <algorithm>
#include <ctime>   // for time()
using namespace std;


struct Car {
    int slotNo;             // Slot number
    string carNumber;       // Vehicle number
    time_t entryTime;       // Entry timestamp
    Car* next;              // Pointer to next car
};


class ParkingLot {
    int capacity;               // total slots
    int occupied;               // used slots
    Car* head;                  // linked list head
    vector<int> freeSlots;      // available slots
    double totalEarnings;       // total money collected

public:
   
    ParkingLot(int cap) {
        capacity = cap;
        occupied = 0;
        head = nullptr;
        totalEarnings = 0.0;

        // Initially all slots are free
        for (int i = 1; i <= capacity; i++) {
            freeSlots.push_back(i);
        }
    }

    
    int getNextSlot() {
        sort(freeSlots.begin(), freeSlots.end()); // keep lowest at front
        int slot = freeSlots.front();
        freeSlots.erase(freeSlots.begin());
        return slot;
    }

   
    void parkCar(string number) {
        if (occupied >= capacity) {
            cout << "❌ Parking Full! Cannot park " << number << endl;
            return;
        }

        int assignedSlot = getNextSlot();

        Car* newCar = new Car();
        newCar->slotNo = assignedSlot;
        newCar->carNumber = number;
        newCar->entryTime = time(0);  // current time
        newCar->next = head;
        head = newCar;

        occupied++;
        cout << "✅ Car " << number << " parked at slot " << newCar->slotNo << " at "
             << ctime(&newCar->entryTime);
    }

   
    void removeCar(string number) {
        if (!head) {
            cout << "❌ No cars parked.\n";
            return;
        }

        Car* temp = head;
        Car* prev = nullptr;

        while (temp != nullptr && temp->carNumber != number) {
            prev = temp;
            temp = temp->next;
        }

        if (!temp) {
            cout << "❌ Car " << number << " not found.\n";
            return;
        }

     
        if (prev == nullptr) {
            head = temp->next;
        } else {
            prev->next = temp->next;
        }

        time_t exitTime = time(0);
        double duration = difftime(exitTime, temp->entryTime) / 60.0; // in minutes
        double fee = (duration / 60.0) * 20.0; // ₹20 per hour
        if (fee < 20) fee = 20; // minimum charge

        cout << "🟢 Car " << number << " removed from slot " << temp->slotNo << endl;
        cout << "⏱ Duration: " << duration << " minutes" << endl;
        cout << "💰 Parking Fee: ₹" << fee << endl;

        totalEarnings += fee;

      
        freeSlots.push_back(temp->slotNo);
        delete temp;
        occupied--;
    }

  
    void display() {
        if (!head) {
            cout << "🚫 No cars parked.\n";
            return;
        }

        cout << "\n🚘 Current Parked Cars:\n";
        Car* temp = head;
        while (temp != nullptr) {
            cout << "Slot " << temp->slotNo << " -> " << temp->carNumber
                 << " ; Parked at :-> " << ctime(&temp->entryTime)<<endl;
            temp = temp->next;
        }
    }


    void showEarnings() {
        cout << "\n💵 Total Earnings: ₹" << totalEarnings << endl;
    }
};


int main() {
    int capacity;
    cout << "Enter parking lot capacity: ";
    cin >> capacity;

    ParkingLot lot(capacity);

    int choice;
    string carNum;

    do {
        cout << "\n=== Smart Parking Lot Menu ===\n";
        cout << "1. Park Car\n2. Remove Car\n3. Display Cars\n4. Show Earnings\n5. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter Car Number: ";
            cin >> carNum;
            lot.parkCar(carNum);
            break;
        case 2:
            cout << "Enter Car Number to remove: ";
            cin >> carNum;
            lot.removeCar(carNum);
            break;
        case 3:
            lot.display();
            break;
        case 4:
            lot.showEarnings();
            break;
        case 5:
            cout << "Exiting...\n";
            break;
        default:
            cout << "Invalid choice!\n";
        }
    } while (choice != 5);

    return 0;
}
