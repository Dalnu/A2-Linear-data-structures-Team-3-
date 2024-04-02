import datetime

class Doctor:
    """Class represent a doctor"""
    def __init__(self, name, specialization):
        self._name = name  # Initialize the name attribute of the doctor
        self.__specialization = specialization  # Initialize the specialization attribute of the doctor

    def get_specialization(self):
        return self.__specialization  # Getter method to access specialization attribute

# Define the PatientRec class to represent patient records
class PatientRec:
    """Class represent the patient records"""

    def __init__(self, name, dob, contactInfo, medicalHistory=None, currCondition=None, docAssigned=None,
                 appointmentDetails=None, medications=None):
        # Initialize patient attributes
        self._name = name  # Patient's name
        self._dob = dob  # Patient's date of birth
        self._contactInfo = contactInfo  # Patient's contact information
        self._medicalHistory = medicalHistory if medicalHistory else []  # Patient's medical history
        self._currCondition = currCondition  # Patient's current medical condition
        self._docAssigned = docAssigned  # Doctor assigned to the patient
        self._appointmentDetails = appointmentDetails  # Details of the patient's appointment
        self._medications = medications if medications else []  # Medications prescribed to the patient

    def update_medical_history(self, new_entry):
        self._medicalHistory.append(new_entry)  # Updating medical history

    def add_medication(self, medication):
        self._medications.append(medication)  # Adding medication

# Define the Node class for the queue implementation
class Node:
    """Class represent the node"""
    def __init__(self, data):
        # Initialize the node with data and a reference to the next node
        self.data = data  # Data stored in the node
        self.next = None  # Reference to the next node

# Define the Queue class to implement a queue using linked list
class Queue:
    """Class represent a queue"""
    def __init__(self):
        # Initialize the queue with front and rear pointers
        self._front = None  # Pointer to the front of the queue
        self._rear = None  # Pointer to the rear of the queue

    def enqueue(self, data):
        new_node = Node(data)  # Create a new node with the given data
        if self._rear is None:
            # If the queue is empty, set both front and rear to the new node
            self._front = self._rear = new_node
            return
        # Otherwise, add the new node to the rear of the queue and update the rear pointer
        self._rear.next = new_node
        self._rear = new_node

    def dequeue(self):
        if self._front is None:
            # If the queue is empty, return None
            return None
        temp = self._front  # Store the front node
        self._front = temp.next  # Move the front pointer to the next node
        if self._front is None:
            # If the queue becomes empty after dequeue, update the rear pointer to None
            self._rear = None
        return temp.data  # Return the data of the dequeued node

    def peek(self):
        return self._front.data if self._front else None  # Return the data of the front node if it exists

    def isEmpty(self):
        return self._front is None  # Return True if the front pointer is None, indicating an empty queue

    def __iter__(self):
        current = self._front
        while current:
            yield current.data
            current = current.next

# Define the PrescriptionStack class to implement a stack for prescriptions
class PrescriptionStack:
    def __init__(self):
        # Initialize the stack with an empty list
        self._stack = []

    def push(self, prescription):
        self._stack.append(prescription)  # Append the prescription to the stack

    def pop(self):
        if self.is_empty():
            # If the stack is empty, return None
            return None
        return self._stack.pop()  # Otherwise, pop and return the top prescription

    def peek(self):
        return self._stack[-1] if not self.is_empty() else None  # Return the top prescription if the stack is not empty

    def is_empty(self):
        return len(self._stack) == 0  # Return True if the stack is empty, False otherwise

class ConsultationQueue:
    """Class represent the queue for managing patient consultations"""

    def __init__(self):
        self._front = None
        self._rear = None

    def enqueue(self, patient):
        new_node = Node(patient)
        if self._rear is None:
            self._front = self._rear = new_node
            return
        self._rear.next = new_node
        self._rear = new_node

    def dequeue(self):
        if self._front is None:
            return None
        temp = self._front
        self._front = temp.next
        if self._front is None:
            self._rear = None
        return temp.data

    def peek(self):
        return self._front.data if self._front else None

    def isEmpty(self):
        return self._front is None

#.......................................................................................

# Add New Patient Record Function
def addPatientRec(patient, patientQueue):
    patientQueue.enqueue(patient)  # Enqueue the new patient into the patient queue
    print("Patient record added successfully.")  # Print a success message

# Update Patient Record Function
def updatePatient(patient, patientQueue):
    updatedPatient = None
    tempQueue = Queue()
    found_patient = False
    while not patientQueue.is_empty():
        currPatient = patientQueue.dequeue()
        if currPatient._name == patient._name:
            found_patient = True
            print("Patient found. Here is the information:")
            print("Name:", currPatient._name)
            print("Date of Birth:", currPatient._dob)
            print("Contact Info:", currPatient._contactInfo)
            print("Medical History:", currPatient._medicalHistory)
            print("Current Condition:", currPatient._currCondition)
            print("Doctor Assigned:", currPatient._docAssigned)
            print("Appointment Details:", currPatient._appointmentDetails)
            print("Medications:", currPatient._medications)

            # Prompt user to select the section to update
            print("\nWhich section would you like to update?")
            print("1. Medical History")
            print("2. Current Condition")
            print("3. Doctor Assigned")
            print("4. Appointment Details")
            print("5. Medications")
            section_choice = input("Enter your choice (1-5): ")

            # Update the selected section
            if section_choice == "1":
                medical_history = input("Enter patient's new medical history (if any): ")
                currPatient.update_medical_history(medical_history)
            elif section_choice == "2":
                curr_condition = input("Enter patient's new current condition (if any): ")
                currPatient.currCondition = curr_condition
            elif section_choice == "3":
                doc_assigned = input("Enter doctor's name: ")
                currPatient.docAssigned = doc_assigned
            elif section_choice == "4":
                appointment_details = input("Enter appointment details: ")
                currPatient.appointmentDetails = appointment_details
            elif section_choice == "5":
                medication = input("Enter new medication: ")
                currPatient.add_medication(medication)
            else:
                print("Invalid choice.")
            updatedPatient = currPatient  # Set updatedPatient to the updated patient
            # Ask the user if they want to update anything else
            choice = input("Do you want to update anything else? (yes/no): ").lower()
            if choice == "no":
                break
        tempQueue.enqueue(currPatient)  # Enqueue the current patient into the temporary queue
    while not tempQueue.isEmpty():
        patientQueue.enqueue(tempQueue.dequeue())  # Re-enqueue patients from the temporary queue back into the patient queue
    if updatedPatient:
        print("Patient record updated successfully.")  # Print a success message if the patient was updated, otherwise print a failure message
    else:
        if not found_patient:
            print("Patient not found.")  # Print a failure message if the patient was not found.

# Schedule Appointment Function
def scheAppoint(patient, doctor, appointment_time):
    patient.appointmentDetails = (doctor._name, appointment_time)  # Set the patient's appointment details
    print("Appointment scheduled successfully.")  # Print a success message

# Issue Prescription Function
def issuPrescription(patient, prescStack, prescription):
    patient._medications.append(prescription)  # Add the prescription to the patient's medications
    prescStack.push(prescription)  # Push the prescription onto the prescription stack
    print("Prescription issued successfully.")  # Print a success message

# Search Patient Function
def searPatient(patientName, patientQueue):
    found = False  # Initialize a flag to track if the patient was found
    patientName = patientName.lower()  # Convert input name to lowercase for case-insensitive comparison
    while not patientQueue.isEmpty():
        currPatient = patientQueue.dequeue()  # Dequeue the current patient
        if currPatient._name.lower() == patientName:  # Compare lowercase patient names
            found = True  # Set found flag to True
            print("Patient Name:", currPatient._name)  # Print the patient's name
            print("Date of Birth:", currPatient._dob)  # Print the patient's date of birth
            print("Contact Info:", currPatient._contactInfo)  # Print the patient's contact info
            print("Medical History:", currPatient._medicalHistory)  # Print the patient's medical history
            print("Current Condition:", currPatient._currCondition)  # Print the patient's current condition
            print("Doctor Assigned:", currPatient._docAssigned)  # Print the doctor assigned to the patient
            print("Appointment Details:", currPatient._appointmentDetails)  # Print the patient's appointment details
            print("Medications:", currPatient._medications)  # Print the patient's medications
            break  # Break out of the loop
    if not found:
        print("Patient not found.")  # Print a failure message if the patient was not found.


# Define the function to remove a patient record
def removePatientRec(patientName, patientQueue):
    tempQueue = Queue()  # Initialize a temporary queue
    found = False  # Flag to track if the patient was found
    while not patientQueue.isEmpty():
        currPatient = patientQueue.dequeue()  # Dequeue the current patient
        if currPatient._name == patientName:  # Check if the current patient matches the provided patient name
            found = True  # Set found flag to True
            print("Patient record removed successfully.")
        else:
            tempQueue.enqueue(currPatient)  # Enqueue patients other than the one to be removed into the temporary queue
    if not found:
        print("Patient not found.")  # Print a failure message if the patient was not found.
    # Re-enqueue patients from the temporary queue back into the patient queue
    while not tempQueue.isEmpty():
        patientQueue.enqueue(tempQueue.dequeue())


# Function to add a patient to the consultation queue
def add_to_consultation_queue(patient_name, patient_queue, consultation_queue):
    found_patient = False
    patient_name = patient_name.lower()  # Convert input name to lowercase for case-insensitive comparison
    for patient in patient_queue:
        if patient._name.lower() == patient_name:  # Compare lowercase patient names
            found_patient = True
            consultation_queue.enqueue(patient)
            print("Patient added to consultation queue successfully.")
            break
    if not found_patient:
        print("Patient not found. Please check the name and try again.")


# Function to consult the next patient in the consultation queue
def consult_all_patients(consultation_queue):
    consulted_patients = []
    while not consultation_queue.isEmpty():
        next_patient = consultation_queue.dequeue()
        consulted_patients.append(next_patient)
    return consulted_patients

#.......................................................................................

patientQueue = Queue()
consultationQueue = ConsultationQueue()

# Define the available services
services = {
    "1": "Add a new patient record",
    "2": "Update an existing patient record",
    "3": "Remove an existing patient record",
    "4": "Schedule an appointment for a patient",
    "5": "Issue a prescription to a patient",
    "6": "Search for a patient and display patient summary",
    "7": "Add patient to consultation queue",
    "8": "Consult next patient",
    "9": "Exit the program"
}


def main():
    prescStack = PrescriptionStack()  # Initialize the prescription stack
    while True:
        choice = Services()
        if not process_choice(choice, prescStack):
            break

def Services():
    print("\nAvailable Services:")
    for key, value in services.items():
        print(f"{key}. {value}")

    while True:
        choice = input("\nPlease select a service (1-9): ")
        if choice.isdigit() and 1 <= int(choice) <= 9:
            return choice
        else:
            print("Invalid choice. Please enter a number between 1 and 9.")


def process_choice(choice, prescStack):
    if choice == "1":
        # Service 1: Add a new patient record
        print("Service 1: Add a new patient record")
        name = input("\nEnter patient's name: ")
        while True:
            dob = input("Enter patient's date of birth (YYYY-MM-DD): ")
            try:
                datetime.datetime.strptime(dob, '%Y-%m-%d')
                break  # Exit the loop if the format is valid
            except ValueError:
                print("Invalid date format. Please enter the date in YYYY-MM-DD format.")

        # Validate phone number format
        while True:
            contact_info = input("Enter patient's contact information (Phone Number): ")
            if len(contact_info) == 10 and contact_info.isdigit():
                break  # Exit the loop if the format is valid
            else:
                print("Invalid phone number format. Please enter a 10-digit number.")

        # Once a valid date of birth and phone number are entered, proceed with creating the patient record
        new_patient = PatientRec(name, dob, contact_info)
        patientQueue.enqueue(new_patient)  # Enqueue the new patient into the patient queue
        print("Patient record added successfully.")
    elif choice == "2":
        # Service 2: Update an existing patient record
        print("Service 2: Update an existing patient record")
        name = input("\nEnter patient's name to update record: ")
        found_patient = False
        # Search for the patient in the queue
        for patient in patientQueue:
            if patient._name == name:
                found_patient = True
                print("Patient found. Here is the information:")
                print("Name:", patient._name)
                print("Date of Birth:", patient._dob)
                print("Contact Info:", patient._contactInfo)
                print("Medical History:", patient._medicalHistory)
                print("Current Condition:", patient._currCondition)
                print("Doctor Assigned:", patient._docAssigned)
                print("Appointment Details:", patient._appointmentDetails)
                print("Medications:", patient._medications)

                # Prompt user to select the section to update
                print("\nWhich section would you like to update?")
                print("1. Medical History")
                print("2. Current Condition")
                print("3. Doctor Assigned")
                print("4. Appointment Details")
                print("5. Medications")
                section_choice = input("Enter your choice (1-5): ")

                # Update the selected section
                if section_choice == "1":
                    medical_history = input("Enter patient's new medical history (if any): ")
                    patient.update_medical_history(medical_history)
                elif section_choice == "2":
                    curr_condition = input("Enter patient's new current condition (if any): ")
                    patient.currCondition = curr_condition
                elif section_choice == "3":
                    doc_assigned = input("Enter doctor's name: ")
                    patient.docAssigned = doc_assigned
                elif section_choice == "4":
                    appointment_details = input("Enter appointment details: ")
                    patient.appointmentDetails = appointment_details
                elif section_choice == "5":
                    medication = input("Enter new medication: ")
                    patient.add_medication(medication)
                else:
                    print("Invalid choice.")
                print("Patient record updated successfully.")
                break

        if not found_patient:
            print("Patient not found.")

    elif choice == "3":
        # Service 3: Remove an existing patient record
        print("Service 3: Remove an existing patient record")
        name = input("\nEnter patient's name to remove record: ")
        removePatientRec(name, patientQueue)
    elif choice == "4":
        # Service 4: Schedule an appointment for a patient
        print("Service 4: Schedule an appointment for a patient")
        name = input("\nEnter patient's name to schedule appointment: ")
        doctor_name = input("Enter doctor's name: ")
        doctor_specialization = input("Enter doctor's specialization: ")  # Ask for doctor's specialization

        # Display timing options to the user
        print("Select appointment time:")
        print("1. 9:00 AM")
        print("2. 11:00 AM")
        print("3. 2:00 PM")
        print("4. 4:00 PM")
        choice = input("Enter your choice (1-4): ")

        # Assign the selected time based on user's choice
        if choice == '1':
            appointment_time = "9:00 AM"
        elif choice == '2':
            appointment_time = "11:00 AM"
        elif choice == '3':
            appointment_time = "2:00 PM"
        elif choice == '4':
            appointment_time = "4:00 PM"
        else:
            print("Invalid choice. Defaulting to 9:00 AM.")
            appointment_time = "9:00 AM"

        patient = PatientRec(name, "", "")
        doctor = Doctor(doctor_name, doctor_specialization)  # Provide both name and specialization
        scheAppoint(patient, doctor, appointment_time)  # Pass appointment_time to scheAppoint function
    elif choice == "5":
        # Service 5: Issue a prescription to a patient
        print("Service 5: Issue a prescription to a patient")
        patient_name = input("\nEnter patient's name: ")
        prescription = input("Enter prescription details: ")

        # Find the patient in the queue
        found_patient = False

        for patient in patientQueue:
            if patient._name == patient_name:
                found_patient = True
                issuPrescription(patient, prescStack, prescription)
                break
        if not found_patient:
            print("Patient not found. Please check the name and try again.")

    elif choice == "6":
        # Service 6: Search for a patient and display patient summary
        print("Service 6: Search for a patient and display patient summary")
        patient_name = input("\nEnter patient's name: ")
        searPatient(patient_name, patientQueue)
    elif choice == "7":
        # Service 7: Add patient to consultation queue
        print("Service 7: Add patient to consultation queue")
        patient_name = input("\nEnter patient's name: ")
        add_to_consultation_queue(patient_name, patientQueue, consultationQueue)
    elif choice == "8":
        # Service 8: Consult next patient
        print("Service 8: Consult next patient")
        consulted_patients = consult_all_patients(consultationQueue)
        if not consulted_patients:
            print("No patients found in the consultation queue.")
        else:
            print("Patients Consulted:")
            for patient in consulted_patients:
                print("Name:", patient._name)
                print("Date of Birth:", patient._dob)
                print("Contact Info:", patient._contactInfo)
                print("Medical History:", patient._medicalHistory)
                print("Current Condition:", patient._currCondition)
                print("Doctor Assigned:", patient._docAssigned)
                print("Appointment Details:", patient._appointmentDetails)
                print("Medications:", patient._medications)
                print()
    elif choice == "9":
        # Service 9: Exit the program
        print("Exiting program. Thank you!")
        return False
    return True

if __name__ == "__main__":
    main()
