# Hospital-system
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

class Patient(Person):
    def __init__(self, name, age, patient_id):
        super().__init__(name, age)
        self.patient_id = patient_id

class Doctor(Person):
    def __init__(self, name, age, specialty):
        super().__init__(name, age)
        self.specialty = specialty

class Appointment:
    def __init__(self, patient, doctor, date):
        self.patient = patient
        self.doctor = doctor
        self.date = date

class HospitalSystem:
    def __init__(self):
        self.patients = []
        self.doctors = []
        self.appointments = []

    def add_patient(self, name, age, patient_id):
        patient = Patient(name, age, patient_id)
        self.patients.append(patient)

    def add_doctor(self, name, age, specialty):
        doctor = Doctor(name, age, specialty)
        self.doctors.append(doctor)

    def book_appointment(self, patient_id, doctor_name, date):
        patient = next((p for p in self.patients if p.patient_id == patient_id), None)
        doctor = next((d for d in self.doctors if d.name == doctor_name), None)

        if patient and doctor:
            appointment = Appointment(patient, doctor, date)
            self.appointments.append(appointment)
            print(f"Appointment booked for {patient.name} with Dr. {doctor.name} on {date}")
        else:
            print("Error: Invalid patient ID or doctor name.")

    def list_appointments(self):
        for a in self.appointments:
            print(f"{a.patient.name} has an appointment with Dr. {a.doctor.name} on {a.date}")

# Example usage
hospital = HospitalSystem()
hospital.add_patient("John Doe", 30, "P001")
hospital.add_doctor("Dr. Smith", 45, "Cardiology")
hospital.book_appointment("P001", "Dr. Smith", "2025-04-15")
hospital.list_appointments()
