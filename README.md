# Pet Grooming Scheduler - Budget-Optimized Azure Portfolio Project

## Project Overview
**Niche Market**: Pet grooming salon management and client booking system
**Timeline**: 4 weeks for MVP implementation
**Budget**: $40-50 total (well under $100 student credits)
**Complexity**: Serverless-first architecture showcasing cost-effective Azure skills

## Why This Project for Your Portfolio?
- **Real business value**: Solves actual scheduling pain points for small businesses
- **Budget-conscious design**: Shows understanding of cost optimization
- **Serverless expertise**: High-demand skill demonstrating modern cloud patterns
- **Hybrid architecture**: Mix of Functions and Containers for optimal resource usage
- **Scalable foundation**: Designed to grow with business needs

---

## Optimized Architecture (Under $15/month)

### Frontend Layer
```
┌─────────────────────────────────────────────────────────┐
│                Static Web App (FREE)                    │
│  • React SPA for pet owners                            │
│  • Admin dashboard for salon managers                  │
│  • Groomer interface for service providers             │
│  • Automatic HTTPS, global CDN, CI/CD from GitHub      │
└─────────────────────────────────────────────────────────┘
```

### API & Business Logic
```
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  User Service   │    │  Pet Service    │    │ Notification    │
│ (Function App)  │    │ (Function App)  │    │ (Function App)  │
│                 │    │                 │    │                 │
│ • Authentication│    │ • Pet profiles  │    │ • Email/SMS     │
│ • User profiles │    │ • Photo upload  │    │ • Reminders     │
│ • Role mgmt     │    │ • Medical notes │    │ • Status updates│
└─────────────────┘    └─────────────────┘    └─────────────────┘
         │                       │                       │
         └───────────────────────┼───────────────────────┘
                                 │
                    ┌─────────────────┐
                    │ Booking Service │
                    │(Container App)  │
                    │                 │
                    │ • Scheduling    │
                    │ • Availability  │
                    │ • Appointments  │
                    │ • Logic Engine  │
                    └─────────────────┘
                                 │
┌─────────────────┐              │              ┌─────────────────┐
│ Payment Service │              │              │Image Processing │
│ (Function App)  │              │              │ (Function App)  │
│                 │              │              │                 │
│ • Stripe mock   │              │              │ • Auto resize   │
│ • Invoicing     │              │              │ • Thumbnails    │
│ • Receipts      │              │              │ • Optimization  │
└─────────────────┘              │              └─────────────────┘
                                 │
                    ┌─────────────────┐
                    │   Azure SQL     │
                    │ Database Basic  │
                    │    ($5/month)   │
                    │                 │
                    │ • Users & Auth  │
                    │ • Pets & Owners │
                    │ • Appointments  │
                    │ • Payments      │
                    └─────────────────┘
```

### Storage & Monitoring
```
┌─────────────────┐              ┌─────────────────┐
│  Blob Storage   │              │ App Insights    │
│   ($2/month)    │              │    (FREE)       │
│                 │              │                 │
│ • Pet photos    │              │ • Performance   │
│ • Documents     │              │ • Error tracking│
│ • Backups       │              │ • Usage metrics │
└─────────────────┘              └─────────────────┘
```

---

## Detailed Service Breakdown

### 1. User Management Service (Azure Function)
**Runtime**: .NET 8 Isolated
**Trigger**: HTTP
**Database**: Azure SQL
**Monthly Cost**: FREE (under 1M executions)

**Responsibilities**:
- User registration and authentication
- Role-based access (customer, groomer, admin)
- Profile management
- Password reset workflows

**Key Endpoints**:
- `POST   /api/auth/login`
- `POST   /api/auth/register`
- `POST   /api/auth/refresh`
- `POST   /api/auth/forgot-password`
- `PUT    /api/auth/reset-password`
- `GET    /api/users/profile`
- `PUT    /api/users/profile`
- `DELETE /api/users/account`

### 2. Pet Management Service (Azure Function) 
**Runtime**: Node.js 18
**Trigger**: HTTP + Blob (for images)
**Database**: Azure SQL + Blob Storage
**Monthly Cost**: FREE (under 1M executions)

**Responsibilities**:
- Pet profile CRUD operations
- Photo upload and management
- Medical history tracking
- Breed-specific service recommendations

**Key Endpoints**:
- `GET    /api/pets/owner/{ownerId}`
- `POST   /api/pets`
- `GET    /api/pets/{petId}`
- `PUT    /api/pets/{petId}`
- `DELETE /api/pets/{petId}`
- `POST   /api/pets/{petId}/photos`
- `GET    /api/pets/{petId}/photos`
- `DELETE /api/pets/{petId}/photos/{photoId}`
- `GET    /api/pets/{petId}/history`
- `POST   /api/pets/{petId}/medical`

### 3. Booking & Scheduling Service (Container App)
**Runtime**: Python FastAPI
**Database**: Azure SQL
**Monthly Cost**: ~$8-12 (0.25 vCPU, 0.5GB RAM)

**Why Container instead of Function**:
- Complex scheduling algorithms need consistent state
- Long-running optimization calculations
- Background processing for availability updates
- WebSocket support for real-time updates

**Responsibilities**:
- Appointment scheduling with conflict resolution
- Availability calculation engine
- Service duration estimation
- Waitlist management

**Key Features**:
- Smart scheduling algorithm considering:
  - Groomer skills and pet breed requirements
  - Service duration and setup time
  - Travel time between appointments
  - Groomer preferences and availability

**Key Endpoints**:
- `GET    /api/availability`
-    `?date=2024-01-15`
-    `&serviceId=123`
-    `&duration=60`
-    `&groomerId=456`
- `POST   /api/appointments`
- `GET    /api/appointments/customer/{customerId}`
- `GET    /api/appointments/groomer/{groomerId}`
- `GET    /api/appointments/{appointmentId}`
- `PUT    /api/appointments/{appointmentId}`
- `DELETE /api/appointments/{appointmentId}`
- `POST   /api/appointments/{appointmentId}/reschedule`
- `PUT    /api/appointments/{appointmentId}/status`

### 4. Notification Service (Azure Function)
**Runtime**: C# Isolated
**Trigger**: Service Bus + Timer
**Integration**: SendGrid (free tier), Twilio trial
**Monthly Cost**: FREE

**Responsibilities**:
- Appointment reminders (24hr, 2hr before)
- Booking confirmations
- Status change notifications
- Marketing communications (with consent)

**Notification Types**:
- Email templates for different scenarios
- SMS for urgent updates
- In-app notifications
- Push notifications (future enhancement)

**Key Endpoints**:
- `POST   /api/notifications/send`
- `GET    /api/notifications/templates`
- `PUT    /api/notifications/preferences`
- `GET    /api/notifications/history/{userId}`

### 5. Payment Processing Service (Azure Function)
**Runtime**: Node.js 18
**Trigger**: HTTP + Service Bus
**Integration**: Stripe test environment
**Monthly Cost**: FREE

**Responsibilities**:
- Payment intent creation and processing
- Invoice generation and management
- Refund processing
- Payment status tracking

**Features**:
- Secure payment handling with Stripe
- Automated invoice generation
- Payment history and receipts
- Subscription management for salons

**Key Endpoints**:
- `POST   /api/payments/intent`
- `POST   /api/payments/confirm`
- `GET    /api/payments/history/{customerId}`
- `POST   /api/payments/refund`
- `GET    /api/invoices/{customerId}`
- `POST   /api/invoices/{appointmentId}`

### 6. Image Processing Service (Azure Function)
**Runtime**: Python 3.11
**Trigger**: Blob Storage events
**Dependencies**: Pillow, OpenCV
**Monthly Cost**: FREE

**Responsibilities**:
- Automatic image resizing and optimization
- Thumbnail generation
- Before/after photo comparisons
- Image metadata extraction

**Processing Pipeline**:
- Original image upload → Blob trigger
- Generate multiple sizes (thumbnail, medium, large)
- Apply watermarks and compression
- Store optimized versions

---

## Database Schema (Azure SQL Basic - $5/month)

### Core Tables
```sql
-- Users and Authentication
Users (Id, Email, PasswordHash, Role, CreatedAt, IsActive)
UserProfiles (UserId, FirstName, LastName, Phone, Address, Preferences)

-- Pet Management
Pets (Id, OwnerId, Name, Breed, Age, Weight, SpecialNotes, PhotoUrls)
PetMedicalHistory (Id, PetId, VaccinationDate, Conditions, Medications)

-- Scheduling
Services (Id, Name, Duration, Price, RequiredSkills)
Groomers (Id, UserId, Skills, Availability, HourlyRate)
Appointments (Id, PetId, GroomerId, ServiceId, DateTime, Status, Notes)
AvailabilitySlots (Id, GroomerId, Date, StartTime, EndTime, IsBooked)

-- Payments
Payments (Id, AppointmentId, Amount, Status, StripePaymentId, CreatedAt)
Invoices (Id, CustomerId, Amount, DueDate, Status, Items)
```

### JSON Columns for Flexibility
```sql
-- Store complex data as JSON to avoid additional tables
ALTER TABLE Pets ADD ExtendedInfo NVARCHAR(MAX) CHECK (ISJSON(ExtendedInfo) = 1)
-- Example: {"allergies": ["shampoo"], "behavior": "friendly", "lastGroomed": "2024-01-15"}

ALTER TABLE UserProfiles ADD Preferences NVARCHAR(MAX) CHECK (ISJSON(Preferences) = 1)
-- Example: {"notifications": {"email": true, "sms": false}, "preferredGroomer": 123}
```

---

## 4-Week Implementation Timeline

### Week 1: Foundation Setup
**Budget Spent**: ~$12
- [x] Create Azure Resource Group
- [x] Deploy Azure SQL Database Basic ($5/month)
- [x] Set up Azure Static Web App (FREE)
- [x] Create Function Apps (FREE)
- [x] Configure GitHub Actions CI/CD
- [x] Build basic React frontend structure
- [x] Implement User Service Function
- [x] Set up Application Insights monitoring

**Deliverables**:
- Working authentication system
- Basic user registration/login
- Infrastructure as Code (Bicep templates)
- CI/CD pipeline

### Week 2: Core Business Logic
**Budget Spent**: ~$15
- [x] Deploy Container App for Booking Service ($8-12/month)
- [x] Create Pet Management Function
- [x] Set up Blob Storage for images ($2/month)
- [x] Implement basic scheduling algorithm
- [x] Build appointment CRUD operations
- [x] Create pet profile management

**Deliverables**:
- Working appointment booking system
- Pet profile management
- Basic scheduling logic
- Image upload functionality

### Week 3: Advanced Features
**Budget Spent**: ~$8
- [x] Implement Notification Service Function
- [x] Add Payment Processing Function (mock)
- [x] Create Image Processing Function
- [x] Set up Service Bus for event messaging (FREE tier)
- [x] Add real-time updates with SignalR (FREE tier)
- [x] Implement reminder system

**Deliverables**:
- Notification system with email/SMS
- Payment processing workflow
- Automated image optimization
- Event-driven architecture

### Week 4: Polish & Production Ready
**Budget Spent**: ~$5
- [x] Add comprehensive error handling
- [x] Implement logging and monitoring
- [x] Create admin dashboard features
- [x] Add data validation and security
- [x] Performance optimization
- [x] Write documentation and README
- [x] Prepare demo environment

**Deliverables**:
- Production-ready application
- Complete documentation
- Demo video and screenshots
- Performance metrics report

**Total 4-Week Cost**: ~$40-50

---

## Cost Breakdown (Monthly after completion)

### Compute Services
- **Azure Static Web Apps**: FREE
- **Azure Functions (5 functions)**: FREE (under 1M executions)
- **Azure Container Apps**: $8-12/month (minimal resources)

### Data & Storage
- **Azure SQL Database Basic**: $5/month (2GB storage)
- **Blob Storage Hot**: $2/month (minimal usage)
- **Service Bus Basic**: FREE (first 12.5M operations)

### Monitoring & Security
- **Application Insights**: FREE (5GB/month)
- **Azure Key Vault**: FREE (10,000 operations)

### **Total Monthly Cost: $15-19**
### **Total Development Cost: $40-50**

---

## Technical Skills Demonstrated

### Cloud Architecture
- **Serverless-first design**: Cost-effective, scalable solutions
- **Hybrid architecture**: Optimal resource allocation (Functions + Containers)
- **Event-driven patterns**: Service Bus messaging, Blob triggers
- **Microservices principles**: Service boundaries, data ownership

### Development Practices
- **Multi-language expertise**: C#, Node.js, Python, React
- **Database design**: Relational modeling with JSON flexibility
- **API design**: RESTful endpoints, OpenAPI documentation
- **Security**: Authentication, authorization, input validation

### DevOps & Operations
- **Infrastructure as Code**: Bicep templates for reproducible deployments
- **CI/CD**: GitHub Actions for automated testing and deployment
- **Monitoring**: Application Insights for performance and error tracking
- **Cost optimization**: Resource sizing and tier selection

### Modern Web Development
- **Frontend**: React with hooks, responsive design, PWA features
- **Real-time features**: SignalR for live updates
- **Image processing**: Automated optimization and resizing
- **Payment integration**: Stripe for secure transactions

---

## Portfolio Presentation Strategy

### The Problem Statement
*"Small pet grooming salons struggle with manual scheduling, leading to double-bookings, missed appointments, and lost revenue. They need an affordable, easy-to-use system that handles complex scheduling requirements."*

### The Solution Architecture
*"I built a serverless-first application using Azure Functions for cost efficiency, with a single Container App for the complex scheduling engine. This hybrid approach demonstrates understanding of both cost optimization and performance requirements."*

### Technical Highlights
- **Smart Cost Management**: Achieved full functionality for under $20/month
- **Scalable Design**: Can handle growth from single salon to franchise
- **Event-Driven**: Loose coupling enables independent service evolution
- **Production Ready**: Comprehensive monitoring, error handling, and security

### Business Impact
- **Cost Savings**: 60% cheaper than traditional hosting approaches
- **Improved Efficiency**: Automated scheduling reduces booking conflicts
- **Better Customer Experience**: Real-time updates and automated reminders
- **Revenue Growth**: Optimized scheduling increases appointment capacity

---

## Demo Script & Screenshots

### Landing Page
- Professional design showcasing salon booking interface
- Clear value proposition and feature highlights
- Mobile-responsive layout

### Customer Journey
1. **Pet Owner Registration**: Simple signup with pet profile creation
2. **Service Selection**: Browse available services with pricing
3. **Scheduling**: Visual calendar with available time slots
4. **Booking Confirmation**: Immediate confirmation with calendar integration
5. **Reminders**: Automated email/SMS notifications

### Admin Dashboard
- **Appointment Overview**: Daily/weekly schedule view
- **Pet Profiles**: Comprehensive pet information and history
- **Analytics**: Booking trends, revenue tracking, popular services
- **Settings**: Service configuration, groomer management

### Technical Demonstrations
- **Real-time Updates**: Show live booking updates across multiple browser tabs
- **Image Processing**: Upload pet photo and show automatic resizing
- **Notification System**: Trigger appointment reminder via admin panel
- **Payment Flow**: Complete booking with simulated payment processing

---


## Success Metrics

### Technical Metrics
- **API Response Time**: < 300ms average
- **Uptime**: 99.5% availability (considering free tiers)
- **Error Rate**: < 1%
- **Cost per User**: < $0.50/month

### Portfolio Metrics
- **GitHub Stars**: Track community interest
- **Demo Engagement**: Time spent on live demo
- **Interview Mentions**: Frequency of project discussion
- **Job Application Success**: Callback rate improvement

---

## Getting Started Checklist

### Prerequisites
- [ ] Azure student account with $100 credits
- [ ] GitHub account for source control
- [ ] Visual Studio Code with Azure extensions
- [ ] Node.js, .NET 8, Python 3.11 installed locally

### Week 1 Tasks
- [ ] Fork starter repository (to be created)
- [ ] Deploy Azure infrastructure using provided Bicep templates
- [ ] Configure local development environment
- [ ] Run initial database migrations
- [ ] Deploy first Function App
- [ ] Verify CI/CD pipeline

### Success Criteria
By the end of 4 weeks, you'll have:
- ✅ A fully functional pet grooming scheduler
- ✅ Comprehensive Azure architecture demonstration
- ✅ Production-ready code with proper documentation
- ✅ Live demo environment for interviews
- ✅ Deep understanding of serverless and container technologies
- ✅ Portfolio piece showcasing real business value
