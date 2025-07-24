# MERN Stack Capstone Project

This assignment focuses on designing, developing, and deploying a comprehensive full-stack MERN application that showcases all the skills you've learned throughout the course.

## Assignment Overview

You will:
1. Plan and design a full-stack MERN application
2. Develop a robust backend with MongoDB, Express.js, and Node.js
3. Create an interactive frontend with React.js
4. Implement testing across the entire application
5. Deploy the application to production

## Getting Started

1. Accept the GitHub Classroom assignment
2. Clone the repository to your local machine
3. Follow the instructions in the `Week8-Assignment.md` file
4. Plan, develop, and deploy your capstone project

## Files Included

- `Week8-Assignment.md`: Detailed assignment instructions

## Requirements

- Node.js (v18 or higher)
- MongoDB (local installation or Atlas account)
- npm or yarn
- Git and GitHub account
- Accounts on deployment platforms (Render/Vercel/Netlify/etc.)

## Project Ideas

The `Week8-Assignment.md` file includes several project ideas, but you're encouraged to develop your own idea that demonstrates your skills and interests.

## Submission

Your project will be automatically submitted when you push to your GitHub Classroom repository. Make sure to:

1. Commit and push your code regularly
2. Include comprehensive documentation
3. Deploy your application and add the live URL to your README.md
4. Create a video demonstration and include the link in your README.md

## Resources

- [MongoDB Documentation](https://docs.mongodb.com/)
- [Express.js Documentation](https://expressjs.com/)
- [React Documentation](https://react.dev/)
- [Node.js Documentation](https://nodejs.org/en/docs/)
- [GitHub Classroom Guide](https://docs.github.com/en/education/manage-coursework-with-github-classroom)
-
- **PROJECT LINK: https://elkanas.netlify.app/**
**src/types/index.ts**
 export interface Patient {
  id: string;
  name: string;
  age: number;
  gender: 'male' | 'female' | 'other';
  phone: string;
  email: string;
  address: string;
  bloodGroup: string;
  emergencyContact: string;
  admissionDate: string;
  status: 'active' | 'discharged' | 'critical';
  assignedDoctor: string;
  department: string;
}

export interface Doctor {
  id: string;
  name: string;
  specialization: string;
  department: string;
  phone: string;
  email: string;
  experience: number;
  availability: 'available' | 'busy' | 'off-duty';
  patientsCount: number;
  rating: number;
}

export interface Appointment {
  id: string;
  patientId: string;
  patientName: string;
  doctorId: string;
  doctorName: string;
  date: string;
  time: string;
  type: 'consultation' | 'follow-up' | 'emergency' | 'surgery';
  status: 'scheduled' | 'completed' | 'cancelled' | 'no-show';
  notes: string;
}

export interface MedicalRecord {
  id: string;
  patientId: string;
  patientName: string;
  doctorId: string;
  doctorName: string;
  date: string;
  diagnosis: string;
  treatment: string;
  medications: string[];
  notes: string;
  followUpDate?: string;
}

export interface Department {
  id: string;
  name: string;
  head: string;
  doctorCount: number;
  patientCount: number;
  bedCount: number;
  availableBeds: number;
  description: string;
}

export interface DashboardStats {
  totalPatients: number;
  totalDoctors: number;
  todayAppointments: number;
  availableBeds: number;
  emergencyCases: number;
  revenue: number;
}

export interface User {
  id: string;
  name: string;
  email: string;
  role: 'admin' | 'doctor' | 'nurse' | 'receptionist' | 'manager';
  department: string;
  status: 'active' | 'inactive' | 'suspended';
  lastLogin: string;
  createdAt: string;
  permissions: string[];
}

export interface SystemSettings {
  hospitalName: string;
  hospitalAddress: string;
  hospitalPhone: string;
  hospitalEmail: string;
  timezone: string;
  currency: string;
  language: string;
  backupFrequency: 'daily' | 'weekly' | 'monthly';
  maintenanceMode: boolean;
  emailNotifications: boolean;
  smsNotifications: boolean;
}

export interface AuditLog {
  id: string;
  userId: string;
  userName: string;
  action: string;
  resource: string;
  timestamp: string;
  ipAddress: string;
  details: string;
}
src/data/mockData.ts
 import { Patient, Doctor, Appointment, MedicalRecord, Department } from '../types';
import { User, SystemSettings, AuditLog } from '../types';

export const mockPatients: Patient[] = [
  {
    id: '1',
    name: 'John Smith',
    age: 45,
    gender: 'male',
    phone: '+1-555-0123',
    email: 'john.smith@email.com',
    address: '123 Main St, City, State 12345',
    bloodGroup: 'A+',
    emergencyContact: '+1-555-0124',
    admissionDate: '2024-01-15',
    status: 'active',
    assignedDoctor: 'Dr. Sarah Johnson',
    department: 'Cardiology'
  },
  {
    id: '2',
    name: 'Emily Davis',
    age: 32,
    gender: 'female',
    phone: '+1-555-0125',
    email: 'emily.davis@email.com',
    address: '456 Oak Ave, City, State 12345',
    bloodGroup: 'B-',
    emergencyContact: '+1-555-0126',
    admissionDate: '2024-01-20',
    status: 'critical',
    assignedDoctor: 'Dr. Michael Chen',
    department: 'Emergency'
  },
  {
    id: '3',
    name: 'Robert Wilson',
    age: 58,
    gender: 'male',
    phone: '+1-555-0127',
    email: 'robert.wilson@email.com',
    address: '789 Pine St, City, State 12345',
    bloodGroup: 'O+',
    emergencyContact: '+1-555-0128',
    admissionDate: '2024-01-18',
    status: 'active',
    assignedDoctor: 'Dr. Lisa Anderson',
    department: 'Orthopedics'
  }
];

export const mockDoctors: Doctor[] = [
  {
    id: '1',
    name: 'Dr. Sarah Johnson',
    specialization: 'Cardiologist',
    department: 'Cardiology',
    phone: '+1-555-1001',
    email: 'sarah.johnson@elkamedicare.com',
    experience: 12,
    availability: 'available',
    patientsCount: 24,
    rating: 4.8
  },
  {
    id: '2',
    name: 'Dr. Michael Chen',
    specialization: 'Emergency Medicine',
    department: 'Emergency',
    phone: '+1-555-1002',
    email: 'michael.chen@elkamedicare.com',
    experience: 8,
    availability: 'busy',
    patientsCount: 18,
    rating: 4.6
  },
  {
    id: '3',
    name: 'Dr. Lisa Anderson',
    specialization: 'Orthopedic Surgeon',
    department: 'Orthopedics',
    phone: '+1-555-1003',
    email: 'lisa.anderson@elkamedicare.com',
    experience: 15,
    availability: 'available',
    patientsCount: 31,
    rating: 4.9
  }
];

export const mockAppointments: Appointment[] = [
  {
    id: '1',
    patientId: '1',
    patientName: 'John Smith',
    doctorId: '1',
    doctorName: 'Dr. Sarah Johnson',
    date: '2024-01-25',
    time: '10:00 AM',
    type: 'consultation',
    status: 'scheduled',
    notes: 'Regular cardiac checkup'
  },
  {
    id: '2',
    patientId: '2',
    patientName: 'Emily Davis',
    doctorId: '2',
    doctorName: 'Dr. Michael Chen',
    date: '2024-01-25',
    time: '2:30 PM',
    type: 'emergency',
    status: 'completed',
    notes: 'Chest pain evaluation'
  }
];

export const mockMedicalRecords: MedicalRecord[] = [
  {
    id: '1',
    patientId: '1',
    patientName: 'John Smith',
    doctorId: '1',
    doctorName: 'Dr. Sarah Johnson',
    date: '2024-01-20',
    diagnosis: 'Hypertension',
    treatment: 'Lifestyle changes and medication',
    medications: ['Lisinopril 10mg', 'Metoprolol 25mg'],
    notes: 'Patient responding well to treatment',
    followUpDate: '2024-02-20'
  }
];

export const mockDepartments: Department[] = [
  {
    id: '1',
    name: 'Cardiology',
    head: 'Dr. Sarah Johnson',
    doctorCount: 5,
    patientCount: 28,
    bedCount: 20,
    availableBeds: 3,
    description: 'Specialized in heart and cardiovascular conditions'
  },
  {
    id: '2',
    name: 'Emergency',
    head: 'Dr. Michael Chen',
    doctorCount: 8,
    patientCount: 45,
    bedCount: 15,
    availableBeds: 2,
    description: 'Emergency care and trauma services'
  },
  {
    id: '3',
    name: 'Orthopedics',
    head: 'Dr. Lisa Anderson',
    doctorCount: 6,
    patientCount: 32,
    bedCount: 25,
    availableBeds: 8,
    description: 'Bone, joint, and musculoskeletal treatments'
  }
];

export const mockUsers: User[] = [
  {
    id: '1',
    name: 'Admin User',
    email: 'admin@elkamedicare.com',
    role: 'admin',
    department: 'Administration',
    status: 'active',
    lastLogin: '2024-01-25T10:30:00Z',
    createdAt: '2024-01-01T00:00:00Z',
    permissions: ['all']
  },
  {
    id: '2',
    name: 'Dr. Sarah Johnson',
    email: 'sarah.johnson@elkamedicare.com',
    role: 'doctor',
    department: 'Cardiology',
    status: 'active',
    lastLogin: '2024-01-25T09:15:00Z',
    createdAt: '2024-01-10T00:00:00Z',
    permissions: ['patients:read', 'patients:write', 'records:read', 'records:write']
  },
  {
    id: '3',
    name: 'Nurse Mary Wilson',
    email: 'mary.wilson@elkamedicare.com',
    role: 'nurse',
    department: 'Emergency',
    status: 'active',
    lastLogin: '2024-01-25T08:45:00Z',
    createdAt: '2024-01-15T00:00:00Z',
    permissions: ['patients:read', 'appointments:read', 'appointments:write']
  },
  {
    id: '4',
    name: 'John Receptionist',
    email: 'john.reception@elkamedicare.com',
    role: 'receptionist',
    department: 'Front Desk',
    status: 'active',
    lastLogin: '2024-01-24T17:30:00Z',
    createdAt: '2024-01-20T00:00:00Z',
    permissions: ['appointments:read', 'appointments:write', 'patients:read']
  }
];

export const mockSystemSettings: SystemSettings = {
  hospitalName: 'Elka Medicare Hospital',
  hospitalAddress: '123 Healthcare Ave, Medical City, MC 12345',
  hospitalPhone: '+1-555-MEDICARE',
  hospitalEmail: 'info@elkamedicare.com',
  timezone: 'America/New_York',
  currency: 'USD',
  language: 'English',
  backupFrequency: 'daily',
  maintenanceMode: false,
  emailNotifications: true,
  smsNotifications: true
};

export const mockAuditLogs: AuditLog[] = [
  {
    id: '1',
    userId: '2',
    userName: 'Dr. Sarah Johnson',
    action: 'UPDATE',
    resource: 'Patient Record',
    timestamp: '2024-01-25T10:15:00Z',
    ipAddress: '192.168.1.100',
    details: 'Updated medical record for patient John Smith'
  },
  {
    id: '2',
    userId: '3',
    userName: 'Nurse Mary Wilson',
    action: 'CREATE',
    resource: 'Appointment',
    timestamp: '2024-01-25T09:30:00Z',
    ipAddress: '192.168.1.101',
    details: 'Scheduled new appointment for Emily Davis'
  },
  {
    id: '3',
    userId: '1',
    userName: 'Admin User',
    action: 'UPDATE',
    resource: 'System Settings',
    timestamp: '2024-01-25T08:00:00Z',
    ipAddress: '192.168.1.50',
    details: 'Updated hospital contact information'
  },
  {
    id: '4',
    userId: '4',
    userName: 'John Receptionist',
    action: 'VIEW',
    resource: 'Patient List',
    timestamp: '2024-01-25T07:45:00Z',
    ipAddress: '192.168.1.102',
    details: 'Accessed patient directory'
  }
];
src/components/Layout.tsx
 import React from 'react';
import { 
  Activity, 
  Users, 
  UserCheck, 
  Calendar, 
  FileText, 
  Building, 
  Menu,
  X,
  Shield,
  LogOut,
  User
} from 'lucide-react';

interface LayoutProps {
  children: React.ReactNode;
  currentPage: string;
  onPageChange: (page: string) => void;
  currentUser: any;
  onLogout: () => void;
}

const Layout: React.FC<LayoutProps> = ({ children, currentPage, onPageChange, currentUser, onLogout }) => {
  const [sidebarOpen, setSidebarOpen] = React.useState(false);

  const menuItems = [
    { id: 'dashboard', label: 'Dashboard', icon: Activity },
    { id: 'patients', label: 'Patients', icon: Users },
    { id: 'doctors', label: 'Doctors', icon: UserCheck },
    { id: 'appointments', label: 'Appointments', icon: Calendar },
    { id: 'records', label: 'Medical Records', icon: FileText },
    { id: 'departments', label: 'Departments', icon: Building },
    ...(currentUser?.role === 'admin' ? [{ id: 'admin', label: 'Administration', icon: Shield }] : []),
  ];

  return (
    <div className="min-h-screen bg-gray-50">
      {/* Mobile sidebar overlay */}
      {sidebarOpen && (
        <div 
          className="fixed inset-0 z-40 bg-black bg-opacity-50 lg:hidden"
          onClick={() => setSidebarOpen(false)}
        />
      )}

      {/* Sidebar */}
      <div className={`fixed inset-y-0 left-0 z-50 w-64 bg-white shadow-lg transform transition-transform duration-300 ease-in-out lg:translate-x-0 ${
        sidebarOpen ? 'translate-x-0' : '-translate-x-full'
      } lg:static lg:inset-0`}>
        <div className="flex items-center justify-between h-16 px-6 border-b border-gray-200">
          <div className="flex items-center space-x-3">
            <div className="w-8 h-8 bg-blue-600 rounded-lg flex items-center justify-center">
              <Activity className="w-5 h-5 text-white" />
            </div>
            <h1 className="text-xl font-bold text-gray-900">Elka Medicare</h1>
          </div>
          <button
            onClick={() => setSidebarOpen(false)}
            className="lg:hidden text-gray-500 hover:text-gray-700"
          >
            <X className="w-6 h-6" />
          </button>
        </div>

        <nav className="mt-6">
          {menuItems.map((item) => {
            const Icon = item.icon;
            return (
              <button
                key={item.id}
                onClick={() => {
                  onPageChange(item.id);
                  setSidebarOpen(false);
                }}
                className={`w-full flex items-center px-6 py-3 text-left transition-colors duration-200 ${
                  currentPage === item.id
                    ? 'bg-blue-50 text-blue-700 border-r-2 border-blue-700'
                    : 'text-gray-700 hover:bg-gray-50 hover:text-blue-700'
                }`}
              >
                <Icon className="w-5 h-5 mr-3" />
                {item.label}
              </button>
            );
          })}
        </nav>

        {/* User Profile & Logout */}
        <div className="absolute bottom-0 left-0 right-0 p-4 border-t border-gray-200 bg-white">
          <div className="flex items-center space-x-3 mb-3">
            <div className="w-10 h-10 bg-blue-100 rounded-full flex items-center justify-center">
              <User className="w-5 h-5 text-blue-600" />
            </div>
            <div className="flex-1 min-w-0">
              <p className="text-sm font-medium text-gray-900 truncate">{currentUser?.name}</p>
              <p className="text-xs text-gray-500 capitalize">{currentUser?.role}</p>
            </div>
          </div>
          <button
            onClick={onLogout}
            className="w-full flex items-center justify-center space-x-2 px-4 py-2 text-sm text-red-600 hover:bg-red-50 rounded-lg transition-colors"
          >
            <LogOut className="w-4 h-4" />
            <span>Sign Out</span>
          </button>
        </div>
      </div>

      {/* Main content */}
      <div className="lg:pl-64">
        {/* Top bar */}
        <div className="flex items-center justify-between h-16 px-6 bg-white border-b border-gray-200">
          <button
            onClick={() => setSidebarOpen(true)}
            className="lg:hidden text-gray-500 hover:text-gray-700"
          >
            <Menu className="w-6 h-6" />
          </button>
          <div className="flex-1 lg:flex-none" />
          <div className="flex items-center space-x-4">
            <div className="flex items-center space-x-3">
              <div className="w-8 h-8 bg-blue-100 rounded-full flex items-center justify-center">
                <User className="w-4 h-4 text-blue-600" />
              </div>
              <div className="hidden sm:block">
                <p className="text-sm font-medium text-gray-900">{currentUser?.name}</p>
                <p className="text-xs text-gray-500 capitalize">{currentUser?.role} • {currentUser?.department}</p>
              </div>
            </div>
            <div className="text-sm text-gray-600">
              Welcome to Elka Medicare
            </div>
          </div>
        </div>

        {/* Page content */}
        <main className="p-6">
          {children}
        </main>
      </div>
    </div>
  );
};

export default Layout;
src/components/Dashboard.tsx
 import React from 'react';
import { 
  Users, 
  UserCheck, 
  Calendar, 
  Bed, 
  AlertCircle, 
  DollarSign,
  TrendingUp,
  Activity
} from 'lucide-react';
import { mockPatients, mockDoctors, mockAppointments, mockDepartments } from '../data/mockData';

const Dashboard: React.FC = () => {
  const stats = {
    totalPatients: mockPatients.length,
    totalDoctors: mockDoctors.length,
    todayAppointments: mockAppointments.filter(apt => apt.date === '2024-01-25').length,
    availableBeds: mockDepartments.reduce((sum, dept) => sum + dept.availableBeds, 0),
    emergencyCases: mockPatients.filter(p => p.status === 'critical').length,
    revenue: 45750
  };

  const recentPatients = mockPatients.slice(0, 3);
  const upcomingAppointments = mockAppointments.slice(0, 3);

  return (
    <div className="space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-3xl font-bold text-gray-900">Dashboard</h1>
        <div className="text-sm text-gray-500">
          Last updated: {new Date().toLocaleString()}
        </div>
      </div>

      {/* Stats Grid */}
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 xl:grid-cols-6 gap-6">
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Total Patients</p>
              <p className="text-2xl font-bold text-gray-900">{stats.totalPatients}</p>
            </div>
            <div className="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
              <Users className="w-6 h-6 text-blue-600" />
            </div>
          </div>
          <div className="mt-4 flex items-center text-sm">
            <TrendingUp className="w-4 h-4 text-green-500 mr-1" />
            <span className="text-green-600">+12% from last month</span>
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Doctors</p>
              <p className="text-2xl font-bold text-gray-900">{stats.totalDoctors}</p>
            </div>
            <div className="w-12 h-12 bg-green-100 rounded-lg flex items-center justify-center">
              <UserCheck className="w-6 h-6 text-green-600" />
            </div>
          </div>
          <div className="mt-4 text-sm text-gray-500">
            All departments covered
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Today's Appointments</p>
              <p className="text-2xl font-bold text-gray-900">{stats.todayAppointments}</p>
            </div>
            <div className="w-12 h-12 bg-purple-100 rounded-lg flex items-center justify-center">
              <Calendar className="w-6 h-6 text-purple-600" />
            </div>
          </div>
          <div className="mt-4 text-sm text-gray-500">
            2 completed, 1 pending
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Available Beds</p>
              <p className="text-2xl font-bold text-gray-900">{stats.availableBeds}</p>
            </div>
            <div className="w-12 h-12 bg-orange-100 rounded-lg flex items-center justify-center">
              <Bed className="w-6 h-6 text-orange-600" />
            </div>
          </div>
          <div className="mt-4 text-sm text-gray-500">
            Out of 60 total beds
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Emergency Cases</p>
              <p className="text-2xl font-bold text-red-600">{stats.emergencyCases}</p>
            </div>
            <div className="w-12 h-12 bg-red-100 rounded-lg flex items-center justify-center">
              <AlertCircle className="w-6 h-6 text-red-600" />
            </div>
          </div>
          <div className="mt-4 text-sm text-red-600">
            Requires immediate attention
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Monthly Revenue</p>
              <p className="text-2xl font-bold text-gray-900">${stats.revenue.toLocaleString()}</p>
            </div>
            <div className="w-12 h-12 bg-indigo-100 rounded-lg flex items-center justify-center">
              <DollarSign className="w-6 h-6 text-indigo-600" />
            </div>
          </div>
          <div className="mt-4 flex items-center text-sm">
            <TrendingUp className="w-4 h-4 text-green-500 mr-1" />
            <span className="text-green-600">+8% from last month</span>
          </div>
        </div>
      </div>

      {/* Recent Activity */}
      <div className="grid grid-cols-1 lg:grid-cols-2 gap-6">
        {/* Recent Patients */}
        <div className="bg-white rounded-xl shadow-sm border border-gray-100">
          <div className="p-6 border-b border-gray-100">
            <h2 className="text-lg font-semibold text-gray-900">Recent Patients</h2>
          </div>
          <div className="p-6 space-y-4">
            {recentPatients.map((patient) => (
              <div key={patient.id} className="flex items-center space-x-4">
                <div className="w-10 h-10 bg-blue-100 rounded-full flex items-center justify-center">
                  <Users className="w-5 h-5 text-blue-600" />
                </div>
                <div className="flex-1">
                  <p className="font-medium text-gray-900">{patient.name}</p>
                  <p className="text-sm text-gray-500">{patient.department} • {patient.assignedDoctor}</p>
                </div>
                <div className={`px-2 py-1 rounded-full text-xs font-medium ${
                  patient.status === 'critical' 
                    ? 'bg-red-100 text-red-800'
                    : patient.status === 'active'
                    ? 'bg-green-100 text-green-800'
                    : 'bg-gray-100 text-gray-800'
                }`}>
                  {patient.status}
                </div>
              </div>
            ))}
          </div>
        </div>

        {/* Upcoming Appointments */}
        <div className="bg-white rounded-xl shadow-sm border border-gray-100">
          <div className="p-6 border-b border-gray-100">
            <h2 className="text-lg font-semibold text-gray-900">Upcoming Appointments</h2>
          </div>
          <div className="p-6 space-y-4">
            {upcomingAppointments.map((appointment) => (
              <div key={appointment.id} className="flex items-center space-x-4">
                <div className="w-10 h-10 bg-purple-100 rounded-full flex items-center justify-center">
                  <Calendar className="w-5 h-5 text-purple-600" />
                </div>
                <div className="flex-1">
                  <p className="font-medium text-gray-900">{appointment.patientName}</p>
                  <p className="text-sm text-gray-500">{appointment.doctorName} • {appointment.time}</p>
                </div>
                <div className={`px-2 py-1 rounded-full text-xs font-medium ${
                  appointment.status === 'scheduled' 
                    ? 'bg-blue-100 text-blue-800'
                    : appointment.status === 'completed'
                    ? 'bg-green-100 text-green-800'
                    : 'bg-gray-100 text-gray-800'
                }`}>
                  {appointment.status}
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>

      {/* Department Overview */}
      <div className="bg-white rounded-xl shadow-sm border border-gray-100">
        <div className="p-6 border-b border-gray-100">
          <h2 className="text-lg font-semibold text-gray-900">Department Overview</h2>
        </div>
        <div className="p-6">
          <div className="grid grid-cols-1 md:grid-cols-3 gap-6">
            {mockDepartments.map((department) => (
              <div key={department.id} className="p-4 border border-gray-200 rounded-lg hover:border-blue-300 transition-colors">
                <div className="flex items-center justify-between mb-3">
                  <h3 className="font-medium text-gray-900">{department.name}</h3>
                  <Activity className="w-5 h-5 text-blue-600" />
                </div>
                <div className="space-y-2 text-sm text-gray-600">
                  <div className="flex justify-between">
                    <span>Head:</span>
                    <span className="font-medium">{department.head}</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Doctors:</span>
                    <span>{department.doctorCount}</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Patients:</span>
                    <span>{department.patientCount}</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Available Beds:</span>
                    <span className="text-green-600">{department.availableBeds}/{department.bedCount}</span>
                  </div>
                </div>
              </div>
            ))}
          </div>
        </div>
      </div>
    </div>
  );
};

export default Dashboard;
src/components/Patients.tsx
  import React, { useState } from 'react';
import { Search, Plus, Eye, Edit, Trash2, Filter, X, Save } from 'lucide-react';
import { Patient } from '../types';
import { mockPatients } from '../data/mockData';

const Patients: React.FC = () => {
  const [patients, setPatients] = useState<Patient[]>(mockPatients);
  const [searchTerm, setSearchTerm] = useState('');
  const [filterStatus, setFilterStatus] = useState<string>('all');
  const [showAddModal, setShowAddModal] = useState(false);
  const [showEditModal, setShowEditModal] = useState(false);
  const [showViewModal, setShowViewModal] = useState(false);
  const [selectedPatient, setSelectedPatient] = useState<Patient | null>(null);
  const [formData, setFormData] = useState<Partial<Patient>>({
    name: '',
    age: 0,
    gender: 'male',
    phone: '',
    email: '',
    address: '',
    bloodGroup: '',
    emergencyContact: '',
    admissionDate: '',
    status: 'active',
    assignedDoctor: '',
    department: ''
  });

  const filteredPatients = patients.filter(patient => {
    const matchesSearch = patient.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         patient.email.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         patient.phone.includes(searchTerm);
    const matchesFilter = filterStatus === 'all' || patient.status === filterStatus;
    return matchesSearch && matchesFilter;
  });

  const getStatusColor = (status: string) => {
    switch (status) {
      case 'active': return 'bg-green-100 text-green-800';
      case 'critical': return 'bg-red-100 text-red-800';
      case 'discharged': return 'bg-gray-100 text-gray-800';
      default: return 'bg-gray-100 text-gray-800';
    }
  };

  const generateId = () => {
    return (patients.length + 1).toString();
  };

  const resetForm = () => {
    setFormData({
      name: '',
      age: 0,
      gender: 'male',
      phone: '',
      email: '',
      address: '',
      bloodGroup: '',
      emergencyContact: '',
      admissionDate: '',
      status: 'active',
      assignedDoctor: '',
      department: ''
    });
  };

  const handleAddPatient = () => {
    setShowAddModal(true);
    resetForm();
  };

  const handleEditPatient = (patient: Patient) => {
    setSelectedPatient(patient);
    setFormData(patient);
    setShowEditModal(true);
  };

  const handleViewPatient = (patient: Patient) => {
    setSelectedPatient(patient);
    setShowViewModal(true);
  };

  const handleDeletePatient = (patientId: string) => {
    if (window.confirm('Are you sure you want to delete this patient?')) {
      setPatients(patients.filter(p => p.id !== patientId));
    }
  };

  const handleSavePatient = () => {
    if (!formData.name || !formData.email || !formData.phone) {
      alert('Please fill in all required fields');
      return;
    }

    if (showAddModal) {
      const newPatient: Patient = {
        ...formData as Patient,
        id: generateId(),
        admissionDate: formData.admissionDate || new Date().toISOString().split('T')[0]
      };
      setPatients([...patients, newPatient]);
      setShowAddModal(false);
    } else if (showEditModal && selectedPatient) {
      setPatients(patients.map(p => 
        p.id === selectedPatient.id ? { ...formData as Patient, id: selectedPatient.id } : p
      ));
      setShowEditModal(false);
    }
    resetForm();
    setSelectedPatient(null);
  };

  const handleCloseModal = () => {
    setShowAddModal(false);
    setShowEditModal(false);
    setShowViewModal(false);
    setSelectedPatient(null);
    resetForm();
  };

  const PatientForm = () => (
    <div className="space-y-4">
      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Full Name *
          </label>
          <input
            type="text"
            value={formData.name}
            onChange={(e) => setFormData({...formData, name: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            placeholder="Enter patient's full name"
          />
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Age *
          </label>
          <input
            type="number"
            value={formData.age}
            onChange={(e) => setFormData({...formData, age: parseInt(e.target.value) || 0})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            placeholder="Enter age"
            min="0"
            max="150"
          />
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Gender *
          </label>
          <select
            value={formData.gender}
            onChange={(e) => setFormData({...formData, gender: e.target.value as 'male' | 'female' | 'other'})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          >
            <option value="male">Male</option>
            <option value="female">Female</option>
            <option value="other">Other</option>
          </select>
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Blood Group
          </label>
          <select
            value={formData.bloodGroup}
            onChange={(e) => setFormData({...formData, bloodGroup: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          >
            <option value="">Select blood group</option>
            <option value="A+">A+</option>
            <option value="A-">A-</option>
            <option value="B+">B+</option>
            <option value="B-">B-</option>
            <option value="AB+">AB+</option>
            <option value="AB-">AB-</option>
            <option value="O+">O+</option>
            <option value="O-">O-</option>
          </select>
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Phone Number *
          </label>
          <input
            type="tel"
            value={formData.phone}
            onChange={(e) => setFormData({...formData, phone: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            placeholder="+1-555-0123"
          />
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Email Address *
          </label>
          <input
            type="email"
            value={formData.email}
            onChange={(e) => setFormData({...formData, email: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            placeholder="patient@email.com"
          />
        </div>
      </div>

      <div>
        <label className="block text-sm font-medium text-gray-700 mb-1">
          Address
        </label>
        <textarea
          value={formData.address}
          onChange={(e) => setFormData({...formData, address: e.target.value})}
          rows={3}
          className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          placeholder="Enter full address"
        />
      </div>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Emergency Contact
          </label>
          <input
            type="tel"
            value={formData.emergencyContact}
            onChange={(e) => setFormData({...formData, emergencyContact: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            placeholder="+1-555-0124"
          />
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Admission Date
          </label>
          <input
            type="date"
            value={formData.admissionDate}
            onChange={(e) => setFormData({...formData, admissionDate: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          />
        </div>
      </div>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Department
          </label>
          <select
            value={formData.department}
            onChange={(e) => setFormData({...formData, department: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          >
            <option value="">Select department</option>
            <option value="Cardiology">Cardiology</option>
            <option value="Emergency">Emergency</option>
            <option value="Orthopedics">Orthopedics</option>
            <option value="Pediatrics">Pediatrics</option>
            <option value="Neurology">Neurology</option>
            <option value="General Medicine">General Medicine</option>
          </select>
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Assigned Doctor
          </label>
          <select
            value={formData.assignedDoctor}
            onChange={(e) => setFormData({...formData, assignedDoctor: e.target.value})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          >
            <option value="">Select doctor</option>
            <option value="Dr. Sarah Johnson">Dr. Sarah Johnson</option>
            <option value="Dr. Michael Chen">Dr. Michael Chen</option>
            <option value="Dr. Lisa Anderson">Dr. Lisa Anderson</option>
            <option value="Dr. Robert Smith">Dr. Robert Smith</option>
            <option value="Dr. Emily Davis">Dr. Emily Davis</option>
          </select>
        </div>
        <div>
          <label className="block text-sm font-medium text-gray-700 mb-1">
            Status
          </label>
          <select
            value={formData.status}
            onChange={(e) => setFormData({...formData, status: e.target.value as 'active' | 'discharged' | 'critical'})}
            className="w-full px-3 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          >
            <option value="active">Active</option>
            <option value="critical">Critical</option>
            <option value="discharged">Discharged</option>
          </select>
        </div>
      </div>
    </div>
  );

  const PatientView = () => (
    selectedPatient && (
      <div className="space-y-6">
        <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
          <div className="space-y-4">
            <div>
              <h3 className="text-lg font-semibold text-gray-900 mb-3">Personal Information</h3>
              <div className="space-y-3">
                <div className="flex justify-between">
                  <span className="text-gray-600">Full Name:</span>
                  <span className="font-medium">{selectedPatient.name}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Age:</span>
                  <span className="font-medium">{selectedPatient.age} years</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Gender:</span>
                  <span className="font-medium capitalize">{selectedPatient.gender}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Blood Group:</span>
                  <span className="font-medium">{selectedPatient.bloodGroup}</span>
                </div>
              </div>
            </div>
            
            <div>
              <h3 className="text-lg font-semibold text-gray-900 mb-3">Contact Information</h3>
              <div className="space-y-3">
                <div className="flex justify-between">
                  <span className="text-gray-600">Phone:</span>
                  <span className="font-medium">{selectedPatient.phone}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Email:</span>
                  <span className="font-medium">{selectedPatient.email}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Emergency Contact:</span>
                  <span className="font-medium">{selectedPatient.emergencyContact}</span>
                </div>
              </div>
            </div>
          </div>

          <div className="space-y-4">
            <div>
              <h3 className="text-lg font-semibold text-gray-900 mb-3">Medical Information</h3>
              <div className="space-y-3">
                <div className="flex justify-between">
                  <span className="text-gray-600">Department:</span>
                  <span className="font-medium">{selectedPatient.department}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Assigned Doctor:</span>
                  <span className="font-medium">{selectedPatient.assignedDoctor}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Admission Date:</span>
                  <span className="font-medium">{new Date(selectedPatient.admissionDate).toLocaleDateString()}</span>
                </div>
                <div className="flex justify-between">
                  <span className="text-gray-600">Status:</span>
                  <span className={`px-2 py-1 rounded-full text-xs font-medium capitalize ${getStatusColor(selectedPatient.status)}`}>
                    {selectedPatient.status}
                  </span>
                </div>
              </div>
            </div>

            <div>
              <h3 className="text-lg font-semibold text-gray-900 mb-3">Address</h3>
              <p className="text-gray-600 bg-gray-50 p-3 rounded-lg">{selectedPatient.address}</p>
            </div>
          </div>
        </div>
      </div>
    )
  );

  return (
    <div className="space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-3xl font-bold text-gray-900">Patients</h1>
        <button
          onClick={handleAddPatient}
          className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2"
        >
          <Plus className="w-5 h-5" />
          <span>Add Patient</span>
        </button>
      </div>

      {/* Search and Filter */}
      <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
        <div className="flex flex-col sm:flex-row space-y-4 sm:space-y-0 sm:space-x-4">
          <div className="flex-1 relative">
            <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
            <input
              type="text"
              placeholder="Search patients by name, email, or phone..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            />
          </div>
          <div className="flex items-center space-x-2">
            <Filter className="w-5 h-5 text-gray-400" />
            <select
              value={filterStatus}
              onChange={(e) => setFilterStatus(e.target.value)}
              className="border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            >
              <option value="all">All Status</option>
              <option value="active">Active</option>
              <option value="critical">Critical</option>
              <option value="discharged">Discharged</option>
            </select>
          </div>
        </div>
      </div>

      {/* Patients Table */}
      <div className="bg-white rounded-xl shadow-sm border border-gray-100 overflow-hidden">
        <div className="overflow-x-auto">
          <table className="w-full">
            <thead className="bg-gray-50 border-b border-gray-200">
              <tr>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Patient</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Age/Gender</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Contact</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Blood Group</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Department</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Doctor</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Status</th>
                <th className="text-left py-4 px-6 font-medium text-gray-900">Actions</th>
              </tr>
            </thead>
            <tbody className="divide-y divide-gray-200">
              {filteredPatients.map((patient) => (
                <tr key={patient.id} className="hover:bg-gray-50 transition-colors">
                  <td className="py-4 px-6">
                    <div>
                      <div className="font-medium text-gray-900">{patient.name}</div>
                      <div className="text-sm text-gray-500">ID: {patient.id}</div>
                    </div>
                  </td>
                  <td className="py-4 px-6">
                    <div className="text-sm">
                      <div>{patient.age} years</div>
                      <div className="text-gray-500 capitalize">{patient.gender}</div>
                    </div>
                  </td>
                  <td className="py-4 px-6">
                    <div className="text-sm">
                      <div>{patient.phone}</div>
                      <div className="text-gray-500">{patient.email}</div>
                    </div>
                  </td>
                  <td className="py-4 px-6">
                    <span className="inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium bg-blue-100 text-blue-800">
                      {patient.bloodGroup}
                    </span>
                  </td>
                  <td className="py-4 px-6 text-sm text-gray-900">
                    {patient.department}
                  </td>
                  <td className="py-4 px-6 text-sm text-gray-900">
                    {patient.assignedDoctor}
                  </td>
                  <td className="py-4 px-6">
                    <span className={`inline-flex items-center px-2.5 py-0.5 rounded-full text-xs font-medium capitalize ${getStatusColor(patient.status)}`}>
                      {patient.status}
                    </span>
                  </td>
                  <td className="py-4 px-6">
                    <div className="flex items-center space-x-2">
                      <button 
                        onClick={() => handleViewPatient(patient)}
                        className="text-blue-600 hover:text-blue-800 transition-colors p-1 hover:bg-blue-50 rounded"
                        title="View Patient"
                      >
                        <Eye className="w-4 h-4" />
                      </button>
                      <button 
                        onClick={() => handleEditPatient(patient)}
                        className="text-yellow-600 hover:text-yellow-800 transition-colors p-1 hover:bg-yellow-50 rounded"
                        title="Edit Patient"
                      >
                        <Edit className="w-4 h-4" />
                      </button>
                      <button 
                        onClick={() => handleDeletePatient(patient.id)}
                        className="text-red-600 hover:text-red-800 transition-colors p-1 hover:bg-red-50 rounded"
                        title="Delete Patient"
                      >
                        <Trash2 className="w-4 h-4" />
                      </button>
                    </div>
                  </td>
                </tr>
              ))}
            </tbody>
          </table>
        </div>
      </div>

      {filteredPatients.length === 0 && (
        <div className="text-center py-12">
          <p className="text-gray-500">No patients found matching your search criteria.</p>
        </div>
      )}

      {/* Add Patient Modal */}
      {showAddModal && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
          <div className="bg-white rounded-xl shadow-xl max-w-4xl w-full max-h-[90vh] overflow-y-auto">
            <div className="flex items-center justify-between p-6 border-b border-gray-200">
              <h2 className="text-xl font-semibold text-gray-900">Add New Patient</h2>
              <button
                onClick={handleCloseModal}
                className="text-gray-400 hover:text-gray-600 transition-colors"
              >
                <X className="w-6 h-6" />
              </button>
            </div>
            <div className="p-6">
              <PatientForm />
            </div>
            <div className="flex items-center justify-end space-x-3 p-6 border-t border-gray-200">
              <button
                onClick={handleCloseModal}
                className="px-4 py-2 text-gray-700 bg-gray-100 rounded-lg hover:bg-gray-200 transition-colors"
              >
                Cancel
              </button>
              <button
                onClick={handleSavePatient}
                className="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2"
              >
                <Save className="w-4 h-4" />
                <span>Add Patient</span>
              </button>
            </div>
          </div>
        </div>
      )}

      {/* Edit Patient Modal */}
      {showEditModal && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
          <div className="bg-white rounded-xl shadow-xl max-w-4xl w-full max-h-[90vh] overflow-y-auto">
            <div className="flex items-center justify-between p-6 border-b border-gray-200">
              <h2 className="text-xl font-semibold text-gray-900">Edit Patient</h2>
              <button
                onClick={handleCloseModal}
                className="text-gray-400 hover:text-gray-600 transition-colors"
              >
                <X className="w-6 h-6" />
              </button>
            </div>
            <div className="p-6">
              <PatientForm />
            </div>
            <div className="flex items-center justify-end space-x-3 p-6 border-t border-gray-200">
              <button
                onClick={handleCloseModal}
                className="px-4 py-2 text-gray-700 bg-gray-100 rounded-lg hover:bg-gray-200 transition-colors"
              >
                Cancel
              </button>
              <button
                onClick={handleSavePatient}
                className="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2"
              >
                <Save className="w-4 h-4" />
                <span>Save Changes</span>
              </button>
            </div>
          </div>
        </div>
      )}

      {/* View Patient Modal */}
      {showViewModal && (
        <div className="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center p-4 z-50">
          <div className="bg-white rounded-xl shadow-xl max-w-4xl w-full max-h-[90vh] overflow-y-auto">
            <div className="flex items-center justify-between p-6 border-b border-gray-200">
              <h2 className="text-xl font-semibold text-gray-900">Patient Details</h2>
              <button
                onClick={handleCloseModal}
                className="text-gray-400 hover:text-gray-600 transition-colors"
              >
                <X className="w-6 h-6" />
              </button>
            </div>
            <div className="p-6">
              <PatientView />
            </div>
            <div className="flex items-center justify-end space-x-3 p-6 border-t border-gray-200">
              <button
                onClick={handleCloseModal}
                className="px-4 py-2 text-gray-700 bg-gray-100 rounded-lg hover:bg-gray-200 transition-colors"
              >
                Close
              </button>
              {selectedPatient && (
                <button
                  onClick={() => {
                    handleCloseModal();
                    handleEditPatient(selectedPatient);
                  }}
                  className="px-4 py-2 bg-blue-600 text-white rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2"
                >
                  <Edit className="w-4 h-4" />
                  <span>Edit Patient</span>
                </button>
              )}
            </div>
          </div>
        </div>
      )}
    </div>
  );
};

export default Patients;
src/components/Doctors.tsx
 import React, { useState } from 'react';
import { Search, Plus, Eye, Edit, Trash2, Filter, Star } from 'lucide-react';
import { Doctor } from '../types';
import { mockDoctors } from '../data/mockData';

const Doctors: React.FC = () => {
  const [doctors, setDoctors] = useState<Doctor[]>(mockDoctors);
  const [searchTerm, setSearchTerm] = useState('');
  const [filterDepartment, setFilterDepartment] = useState<string>('all');
  const [filterAvailability, setFilterAvailability] = useState<string>('all');

  const filteredDoctors = doctors.filter(doctor => {
    const matchesSearch = doctor.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         doctor.specialization.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         doctor.email.toLowerCase().includes(searchTerm.toLowerCase());
    const matchesDepartment = filterDepartment === 'all' || doctor.department === filterDepartment;
    const matchesAvailability = filterAvailability === 'all' || doctor.availability === filterAvailability;
    return matchesSearch && matchesDepartment && matchesAvailability;
  });

  const getAvailabilityColor = (availability: string) => {
    switch (availability) {
      case 'available': return 'bg-green-100 text-green-800';
      case 'busy': return 'bg-yellow-100 text-yellow-800';
      case 'off-duty': return 'bg-gray-100 text-gray-800';
      default: return 'bg-gray-100 text-gray-800';
    }
  };

  const renderStars = (rating: number) => {
    return Array.from({ length: 5 }, (_, i) => (
      <Star
        key={i}
        className={`w-4 h-4 ${i < Math.floor(rating) ? 'text-yellow-400 fill-current' : 'text-gray-300'}`}
      />
    ));
  };

  return (
    <div className="space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-3xl font-bold text-gray-900">Doctors</h1>
        <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2">
          <Plus className="w-5 h-5" />
          <span>Add Doctor</span>
        </button>
      </div>

      {/* Search and Filter */}
      <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
        <div className="flex flex-col lg:flex-row space-y-4 lg:space-y-0 lg:space-x-4">
          <div className="flex-1 relative">
            <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
            <input
              type="text"
              placeholder="Search doctors by name, specialization, or email..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            />
          </div>
          <div className="flex items-center space-x-4">
            <div className="flex items-center space-x-2">
              <Filter className="w-5 h-5 text-gray-400" />
              <select
                value={filterDepartment}
                onChange={(e) => setFilterDepartment(e.target.value)}
                className="border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
              >
                <option value="all">All Departments</option>
                <option value="Cardiology">Cardiology</option>
                <option value="Emergency">Emergency</option>
                <option value="Orthopedics">Orthopedics</option>
              </select>
            </div>
            <select
              value={filterAvailability}
              onChange={(e) => setFilterAvailability(e.target.value)}
              className="border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            >
              <option value="all">All Availability</option>
              <option value="available">Available</option>
              <option value="busy">Busy</option>
              <option value="off-duty">Off Duty</option>
            </select>
          </div>
        </div>
      </div>

      {/* Doctors Grid */}
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {filteredDoctors.map((doctor) => (
          <div key={doctor.id} className="bg-white rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
            <div className="p-6">
              <div className="flex items-center justify-between mb-4">
                <div className="w-16 h-16 bg-blue-100 rounded-full flex items-center justify-center">
                  <span className="text-xl font-semibold text-blue-600">
                    {doctor.name.split(' ').map(n => n[0]).join('')}
                  </span>
                </div>
                <span className={`px-2 py-1 rounded-full text-xs font-medium capitalize ${getAvailabilityColor(doctor.availability)}`}>
                  {doctor.availability.replace('-', ' ')}
                </span>
              </div>

              <div className="space-y-3">
                <div>
                  <h3 className="text-lg font-semibold text-gray-900">{doctor.name}</h3>
                  <p className="text-sm text-gray-600">{doctor.specialization}</p>
                </div>

                <div className="space-y-2 text-sm text-gray-600">
                  <div className="flex justify-between">
                    <span>Department:</span>
                    <span className="font-medium">{doctor.department}</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Experience:</span>
                    <span>{doctor.experience} years</span>
                  </div>
                  <div className="flex justify-between">
                    <span>Patients:</span>
                    <span>{doctor.patientsCount}</span>
                  </div>
                  <div className="flex justify-between items-center">
                    <span>Rating:</span>
                    <div className="flex items-center space-x-1">
                      <div className="flex">{renderStars(doctor.rating)}</div>
                      <span className="text-xs">({doctor.rating})</span>
                    </div>
                  </div>
                </div>

                <div className="pt-3 border-t border-gray-100">
                  <div className="text-sm text-gray-600 mb-3">
                    <div>{doctor.phone}</div>
                    <div>{doctor.email}</div>
                  </div>
                  
                  <div className="flex items-center space-x-2">
                    <button className="flex-1 bg-blue-50 text-blue-600 px-3 py-2 rounded-lg hover:bg-blue-100 transition-colors flex items-center justify-center space-x-1">
                      <Eye className="w-4 h-4" />
                      <span>View</span>
                    </button>
                    <button className="flex-1 bg-gray-50 text-gray-600 px-3 py-2 rounded-lg hover:bg-gray-100 transition-colors flex items-center justify-center space-x-1">
                      <Edit className="w-4 h-4" />
                      <span>Edit</span>
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        ))}
      </div>

      {filteredDoctors.length === 0 && (
        <div className="text-center py-12">
          <p className="text-gray-500">No doctors found matching your search criteria.</p>
        </div>
      )}
    </div>
  );
};

export default Doctors;
 src/components/Appointments.tsx
  import React, { useState } from 'react';
import { Search, Plus, Calendar, Clock, Filter, Eye, Edit, Trash2 } from 'lucide-react';
import { Appointment } from '../types';
import { mockAppointments } from '../data/mockData';

const Appointments: React.FC = () => {
  const [appointments, setAppointments] = useState<Appointment[]>(mockAppointments);
  const [searchTerm, setSearchTerm] = useState('');
  const [filterStatus, setFilterStatus] = useState<string>('all');
  const [filterType, setFilterType] = useState<string>('all');

  const filteredAppointments = appointments.filter(appointment => {
    const matchesSearch = appointment.patientName.toLowerCase().includes(searchTerm.toLowerCase()) ||
                         appointment.doctorName.toLowerCase().includes(searchTerm.toLowerCase());
    const matchesStatus = filterStatus === 'all' || appointment.status === filterStatus;
    const matchesType = filterType === 'all' || appointment.type === filterType;
    return matchesSearch && matchesStatus && matchesType;
  });

  const getStatusColor = (status: string) => {
    switch (status) {
      case 'scheduled': return 'bg-blue-100 text-blue-800';
      case 'completed': return 'bg-green-100 text-green-800';
      case 'cancelled': return 'bg-red-100 text-red-800';
      case 'no-show': return 'bg-gray-100 text-gray-800';
      default: return 'bg-gray-100 text-gray-800';
    }
  };

  const getTypeColor = (type: string) => {
    switch (type) {
      case 'consultation': return 'bg-blue-100 text-blue-800';
      case 'follow-up': return 'bg-green-100 text-green-800';
      case 'emergency': return 'bg-red-100 text-red-800';
      case 'surgery': return 'bg-purple-100 text-purple-800';
      default: return 'bg-gray-100 text-gray-800';
    }
  };

  return (
    <div className="space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-3xl font-bold text-gray-900">Appointments</h1>
        <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2">
          <Plus className="w-5 h-5" />
          <span>Schedule Appointment</span>
        </button>
      </div>

      {/* Search and Filter */}
      <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
        <div className="flex flex-col lg:flex-row space-y-4 lg:space-y-0 lg:space-x-4">
          <div className="flex-1 relative">
            <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
            <input
              type="text"
              placeholder="Search by patient or doctor name..."
              value={searchTerm}
              onChange={(e) => setSearchTerm(e.target.value)}
              className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            />
          </div>
          <div className="flex items-center space-x-4">
            <div className="flex items-center space-x-2">
              <Filter className="w-5 h-5 text-gray-400" />
              <select
                value={filterStatus}
                onChange={(e) => setFilterStatus(e.target.value)}
                className="border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
              >
                <option value="all">All Status</option>
                <option value="scheduled">Scheduled</option>
                <option value="completed">Completed</option>
                <option value="cancelled">Cancelled</option>
                <option value="no-show">No Show</option>
              </select>
            </div>
            <select
              value={filterType}
              onChange={(e) => setFilterType(e.target.value)}
              className="border border-gray-300 rounded-lg px-3 py-2 focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
            >
              <option value="all">All Types</option>
              <option value="consultation">Consultation</option>
              <option value="follow-up">Follow-up</option>
              <option value="emergency">Emergency</option>
              <option value="surgery">Surgery</option>
            </select>
          </div>
        </div>
      </div>

      {/* Appointments List */}
      <div className="space-y-4">
        {filteredAppointments.map((appointment) => (
          <div key={appointment.id} className="bg-white rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
            <div className="p-6">
              <div className="flex flex-col lg:flex-row lg:items-center lg:justify-between space-y-4 lg:space-y-0">
                <div className="flex-1 space-y-3">
                  <div className="flex items-center space-x-4">
                    <div className="w-12 h-12 bg-blue-100 rounded-full flex items-center justify-center">
                      <Calendar className="w-6 h-6 text-blue-600" />
                    </div>
                    <div>
                      <h3 className="text-lg font-semibold text-gray-900">{appointment.patientName}</h3>
                      <p className="text-sm text-gray-600">with {appointment.doctorName}</p>
                    </div>
                  </div>

                  <div className="grid grid-cols-1 md:grid-cols-3 gap-4 text-sm">
                    <div className="flex items-center space-x-2">
                      <Calendar className="w-4 h-4 text-gray-400" />
                      <span className="text-gray-600">Date:</span>
                      <span className="font-medium">{new Date(appointment.date).toLocaleDateString()}</span>
                    </div>
                    <div className="flex items-center space-x-2">
                      <Clock className="w-4 h-4 text-gray-400" />
                      <span className="text-gray-600">Time:</span>
                      <span className="font-medium">{appointment.time}</span>
                    </div>
                    <div className="flex items-center space-x-2">
                      <span className="text-gray-600">ID:</span>
                      <span className="font-medium">#{appointment.id}</span>
                    </div>
                  </div>

                  {appointment.notes && (
                    <div className="text-sm">
                      <span className="text-gray-600">Notes: </span>
                      <span className="text-gray-900">{appointment.notes}</span>
                    </div>
                  )}
                </div>

                <div className="flex flex-col sm:flex-row items-start sm:items-center space-y-3 sm:space-y-0 sm:space-x-4">
                  <div className="flex items-center space-x-2">
                    <span className={`px-3 py-1 rounded-full text-xs font-medium capitalize ${getTypeColor(appointment.type)}`}>
                      {appointment.type}
                    </span>
                    <span className={`px-3 py-1 rounded-full text-xs font-medium capitalize ${getStatusColor(appointment.status)}`}>
                      {appointment.status}
                    </span>
                  </div>

                  <div className="flex items-center space-x-2">
                    <button className="text-blue-600 hover:text-blue-800 transition-colors p-2 hover:bg-blue-50 rounded-lg">
                      <Eye className="w-4 h-4" />
                    </button>
                    <button className="text-yellow-600 hover:text-yellow-800 transition-colors p-2 hover:bg-yellow-50 rounded-lg">
                      <Edit className="w-4 h-4" />
                    </button>
                    <button className="text-red-600 hover:text-red-800 transition-colors p-2 hover:bg-red-50 rounded-lg">
                      <Trash2 className="w-4 h-4" />
                    </button>
                  </div>
                </div>
              </div>
            </div>
          </div>
        ))}
      </div>

      {filteredAppointments.length === 0 && (
        <div className="text-center py-12">
          <Calendar className="w-16 h-16 text-gray-300 mx-auto mb-4" />
          <p className="text-gray-500">No appointments found matching your search criteria.</p>
        </div>
      )}
    </div>
  );
};

export default Appointments;
src/components/MedicalRecords.tsx
  import React, { useState } from 'react';
import { Search, Plus, FileText, Calendar, Filter, Eye, Edit, Download } from 'lucide-react';
import { MedicalRecord } from '../types';
import { mockMedicalRecords } from '../data/mockData';

const MedicalRecords: React.FC = () => {
  const [records, setRecords] = useState<MedicalRecord[]>(mockMedicalRecords);
  const [searchTerm, setSearchTerm] = useState('');

  const filteredRecords = records.filter(record => 
    record.patientName.toLowerCase().includes(searchTerm.toLowerCase()) ||
    record.doctorName.toLowerCase().includes(searchTerm.toLowerCase()) ||
    record.diagnosis.toLowerCase().includes(searchTerm.toLowerCase())
  );

  return (
    <div className="space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-3xl font-bold text-gray-900">Medical Records</h1>
        <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2">
          <Plus className="w-5 h-5" />
          <span>Add Record</span>
        </button>
      </div>

      {/* Search */}
      <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
        <div className="relative">
          <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
          <input
            type="text"
            placeholder="Search records by patient, doctor, or diagnosis..."
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
            className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          />
        </div>
      </div>

      {/* Records List */}
      <div className="space-y-4">
        {filteredRecords.map((record) => (
          <div key={record.id} className="bg-white rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
            <div className="p-6">
              <div className="flex flex-col lg:flex-row space-y-4 lg:space-y-0 lg:space-x-6">
                <div className="flex items-start space-x-4">
                  <div className="w-12 h-12 bg-green-100 rounded-full flex items-center justify-center">
                    <FileText className="w-6 h-6 text-green-600" />
                  </div>
                  <div className="flex-1">
                    <h3 className="text-lg font-semibold text-gray-900">{record.patientName}</h3>
                    <p className="text-sm text-gray-600">Treated by {record.doctorName}</p>
                    <div className="flex items-center space-x-4 mt-2 text-sm text-gray-500">
                      <div className="flex items-center space-x-1">
                        <Calendar className="w-4 h-4" />
                        <span>{new Date(record.date).toLocaleDateString()}</span>
                      </div>
                      <span>Record ID: #{record.id}</span>
                    </div>
                  </div>
                </div>

                <div className="flex-1 space-y-4">
                  <div className="grid grid-cols-1 md:grid-cols-2 gap-4">
                    <div>
                      <h4 className="text-sm font-medium text-gray-900 mb-2">Diagnosis</h4>
                      <p className="text-sm text-gray-600 bg-gray-50 p-3 rounded-lg">{record.diagnosis}</p>
                    </div>
                    <div>
                      <h4 className="text-sm font-medium text-gray-900 mb-2">Treatment</h4>
                      <p className="text-sm text-gray-600 bg-gray-50 p-3 rounded-lg">{record.treatment}</p>
                    </div>
                  </div>

                  {record.medications.length > 0 && (
                    <div>
                      <h4 className="text-sm font-medium text-gray-900 mb-2">Medications</h4>
                      <div className="flex flex-wrap gap-2">
                        {record.medications.map((medication, index) => (
                          <span key={index} className="px-2 py-1 bg-blue-100 text-blue-800 text-xs rounded-full">
                            {medication}
                          </span>
                        ))}
                      </div>
                    </div>
                  )}

                  {record.notes && (
                    <div>
                      <h4 className="text-sm font-medium text-gray-900 mb-2">Notes</h4>
                      <p className="text-sm text-gray-600 bg-gray-50 p-3 rounded-lg">{record.notes}</p>
                    </div>
                  )}

                  {record.followUpDate && (
                    <div className="flex items-center space-x-2 text-sm">
                      <Calendar className="w-4 h-4 text-orange-500" />
                      <span className="text-gray-600">Follow-up scheduled:</span>
                      <span className="font-medium text-orange-600">
                        {new Date(record.followUpDate).toLocaleDateString()}
                      </span>
                    </div>
                  )}
                </div>

                <div className="flex flex-col space-y-2">
                  <button className="flex items-center space-x-2 px-3 py-2 text-blue-600 hover:bg-blue-50 rounded-lg transition-colors">
                    <Eye className="w-4 h-4" />
                    <span>View</span>
                  </button>
                  <button className="flex items-center space-x-2 px-3 py-2 text-yellow-600 hover:bg-yellow-50 rounded-lg transition-colors">
                    <Edit className="w-4 h-4" />
                    <span>Edit</span>
                  </button>
                  <button className="flex items-center space-x-2 px-3 py-2 text-green-600 hover:bg-green-50 rounded-lg transition-colors">
                    <Download className="w-4 h-4" />
                    <span>Export</span>
                  </button>
                </div>
              </div>
            </div>
          </div>
        ))}
      </div>

      {filteredRecords.length === 0 && (
        <div className="text-center py-12">
          <FileText className="w-16 h-16 text-gray-300 mx-auto mb-4" />
          <p className="text-gray-500">No medical records found matching your search criteria.</p>
        </div>
      )}
    </div>
  );
};

export default MedicalRecords;
src/components/Departments.tsx
  import React, { useState } from 'react';
import { Search, Plus, Building, Users, UserCheck, Bed, Activity, Eye, Edit } from 'lucide-react';
import { Department } from '../types';
import { mockDepartments } from '../data/mockData';

const Departments: React.FC = () => {
  const [departments, setDepartments] = useState<Department[]>(mockDepartments);
  const [searchTerm, setSearchTerm] = useState('');

  const filteredDepartments = departments.filter(department =>
    department.name.toLowerCase().includes(searchTerm.toLowerCase()) ||
    department.head.toLowerCase().includes(searchTerm.toLowerCase()) ||
    department.description.toLowerCase().includes(searchTerm.toLowerCase())
  );

  const totalStats = departments.reduce((acc, dept) => ({
    totalDoctors: acc.totalDoctors + dept.doctorCount,
    totalPatients: acc.totalPatients + dept.patientCount,
    totalBeds: acc.totalBeds + dept.bedCount,
    availableBeds: acc.availableBeds + dept.availableBeds,
  }), { totalDoctors: 0, totalPatients: 0, totalBeds: 0, availableBeds: 0 });

  return (
    <div className="space-y-6">
      <div className="flex items-center justify-between">
        <h1 className="text-3xl font-bold text-gray-900">Departments</h1>
        <button className="bg-blue-600 text-white px-4 py-2 rounded-lg hover:bg-blue-700 transition-colors flex items-center space-x-2">
          <Plus className="w-5 h-5" />
          <span>Add Department</span>
        </button>
      </div>

      {/* Overview Stats */}
      <div className="grid grid-cols-1 md:grid-cols-4 gap-6">
        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Total Departments</p>
              <p className="text-2xl font-bold text-gray-900">{departments.length}</p>
            </div>
            <Building className="w-8 h-8 text-blue-600" />
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Total Doctors</p>
              <p className="text-2xl font-bold text-gray-900">{totalStats.totalDoctors}</p>
            </div>
            <UserCheck className="w-8 h-8 text-green-600" />
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Total Patients</p>
              <p className="text-2xl font-bold text-gray-900">{totalStats.totalPatients}</p>
            </div>
            <Users className="w-8 h-8 text-purple-600" />
          </div>
        </div>

        <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
          <div className="flex items-center justify-between">
            <div>
              <p className="text-sm font-medium text-gray-600">Available Beds</p>
              <p className="text-2xl font-bold text-gray-900">{totalStats.availableBeds}</p>
            </div>
            <Bed className="w-8 h-8 text-orange-600" />
          </div>
        </div>
      </div>

      {/* Search */}
      <div className="bg-white p-6 rounded-xl shadow-sm border border-gray-100">
        <div className="relative">
          <Search className="absolute left-3 top-1/2 transform -translate-y-1/2 text-gray-400 w-5 h-5" />
          <input
            type="text"
            placeholder="Search departments by name, head, or description..."
            value={searchTerm}
            onChange={(e) => setSearchTerm(e.target.value)}
            className="w-full pl-10 pr-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
          />
        </div>
      </div>

      {/* Departments Grid */}
      <div className="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        {filteredDepartments.map((department) => (
          <div key={department.id} className="bg-white rounded-xl shadow-sm border border-gray-100 hover:shadow-md transition-shadow">
            <div className="p-6">
              <div className="flex items-center justify-between mb-4">
                <div className="w-12 h-12 bg-blue-100 rounded-lg flex items-center justify-center">
                  <Building className="w-6 h-6 text-blue-600" />
                </div>
                <div className="flex items-center space-x-2">
                  <button className="text-blue-600 hover:text-blue-800 transition-colors">
                    <Eye className="w-4 h-4" />
                  </button>
                  <button className="text-yellow-600 hover:text-yellow-800 transition-colors">
                    <Edit className="w-4 h-4" />
                  </button>
                </div>
              </div>

              <div className="space-y-4">
                <div>
                  <h3 className="text-lg font-semibold text-gray-900">{department.name}</h3>
                  <p className="text-sm text-gray-600">Head: {department.head}</p>
                </div>

                <p className="text-sm text-gray-600 leading-relaxed">
                  {department.description}
                </p>

                <div className="grid grid-cols-2 gap-4 text-sm">
                  <div className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div className="flex items-center space-x-2">
                      <UserCheck className="w-4 h-4 text-green-600" />
                      <span className="text-gray-600">Doctors</span>
                    </div>
                    <span className="font-semibold text-gray-900">{department.doctorCount}</span>
                  </div>

                  <div className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div className="flex items-center space-x-2">
                      <Users className="w-4 h-4 text-purple-600" />
                      <span className="text-gray-600">Patients</span>
                    </div>
                    <span className="font-semibold text-gray-900">{department.patientCount}</span>
                  </div>

                  <div className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div className="flex items-center space-x-2">
                      <Bed className="w-4 h-4 text-orange-600" />
                      <span className="text-gray-600">Total Beds</span>
                    </div>
                    <span className="font-semibold text-gray-900">{department.bedCount}</span>
                  </div>

                  <div className="flex items-center justify-between p-3 bg-gray-50 rounded-lg">
                    <div className="flex items-center space-x-2">
                      <Activity className="w-4 h-4 text-green-600" />
                      <span className="text-gray-600">Available</span>
                    </div>
                    <span className="font-semibold text-green-600">{department.availableBeds}</span>
                  </div>
                </div>

                <div className="pt-4 border-t border-gray-100">
                  <div className="w-full bg-gray-200 rounded-full h-2">
                    <div 
                      className="bg-blue-600 h-2 rounded-full transition-all duration-300"
                      style={{ 
                        width: `${((department.bedCount - department.availableBeds) / department.bedCount) * 100}%` 
                      }}
                    ></div>
                  </div>
                  <div className="flex justify-between text-xs text-gray-500 mt-1">
                    <span>Bed Occupancy</span>
                    <span>{Math.round(((department.bedCount - department.availableBeds) / department.bedCount) * 100)}%</span>
                  </div>
                </div>
              </div>
            </div>
          </div>
        ))}
      </div>

      {filteredDepartments.length === 0 && (
        <div className="text-center py-12">
          <Building className="w-16 h-16 text-gray-300 mx-auto mb-4" />
          <p className="text-gray-500">No departments found matching your search criteria.</p>
        </div>
      )}
    </div>
  );
};

export default Departments;
src/App.tsx
 import React, { useState } from 'react';
import Login from './components/Login';
import Layout from './components/Layout';
import Dashboard from './components/Dashboard';
import Patients from './components/Patients';
import Doctors from './components/Doctors';
import Appointments from './components/Appointments';
import MedicalRecords from './components/MedicalRecords';
import Departments from './components/Departments';
import Admin from './components/Admin';

function App() {
  const [currentPage, setCurrentPage] = useState('dashboard');
  const [currentUser, setCurrentUser] = useState<any>(null);
  const [isAuthenticated, setIsAuthenticated] = useState(false);

  const handleLogin = (user: any) => {
    setCurrentUser(user);
    setIsAuthenticated(true);
    // Reset to dashboard when logging in
    setCurrentPage('dashboard');
  };

  const handleLogout = () => {
    setCurrentUser(null);
    setIsAuthenticated(false);
    setCurrentPage('dashboard');
  };

  const renderCurrentPage = () => {
    // Restrict admin page to admin users only
    if (currentPage === 'admin' && currentUser?.role !== 'admin') {
      return <Dashboard />;
    }

    switch (currentPage) {
      case 'dashboard':
        return <Dashboard />;
      case 'patients':
        return <Patients />;
      case 'doctors':
        return <Doctors />;
      case 'appointments':
        return <Appointments />;
      case 'records':
        return <MedicalRecords />;
      case 'departments':
        return <Departments />;
      case 'admin':
        return <Admin />;
      default:
        return <Dashboard />;
    }
  };

  // Show login page if not authenticated
  if (!isAuthenticated) {
    return <Login onLogin={handleLogin} />;
  }

  return (
    <Layout 
      currentPage={currentPage} 
      onPageChange={setCurrentPage}
      currentUser={currentUser}
      onLogout={handleLogout}
    >
      {renderCurrentPage()}
    </Layout>
  );
}

export default App;
index.html
  <!doctype html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <link rel="icon" type="image/svg+xml" href="/vite.svg" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Elka Medicare - Hospital Management System</title>
    <meta name="description" content="Complete hospital management system for healthcare providers">
  </head>
  <body>
    <div id="root"></div>
    <script type="module" src="/src/main.tsx"></script>
  </body>
</html>
