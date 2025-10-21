<div align="center">
  
![GitHub repo size](https://img.shields.io/github/repo-size/RanitDERIA/tata-rfp?color=yellow)
![GitHub stars](https://img.shields.io/github/stars/RanitDERIA/tata-rfp?style=social)
![GitHub forks](https://img.shields.io/github/forks/RanitDERIA/tata-rfp?style=social)

[![Twitter Follow](https://img.shields.io/twitter/follow/DeriaRanit?style=social)](https://twitter.com/intent/follow?screen_name=DeriaRanit)
[![LinkedIn](https://img.shields.io/badge/LinkedIn%20%40ranit--deria-blue?style=flat-square)](https://www.linkedin.com/in/ranit-deria-916864257/)


  <br />
  <br />
  
  <p align="center">
  <img src="readme-assets/brand1.png"/>
  </p>




  <h2 align="center">AutoRFP - AI-Powered RFP Response Platform</h2>

AutoRFP is an intelligent platform that automates RFP (Request for Proposal) response generation using advanced AI. Built with Next.js 15 and powered by LlamaIndex, it helps organizations respond to RFPs 80% faster by automatically extracting questions from documents and generating contextual responses based on your knowledge base.<br />

<br/>
<img src="./readme-assets/AutoRFP.png" alt="AutoRFP Demo Screenshot"/>
</div>

<br>

<div align="center">
  <img src="./readme-assets/AutoRFP (1).png" alt="Screenshot 1" width="19%"/>
  <img src="./readme-assets/AutoRFP (2).png" alt="Screenshot 2" width="19%"/>
  <img src="./readme-assets/AutoRFP (5).png" alt="Screenshot 3" width="19%"/>
  <img src="./readme-assets/AutoRFP (4).png" alt="Screenshot 4" width="19%"/>
  <img src="./readme-assets/AutoRFP (3).png" alt="Screenshot 5" width="19%"/>
</div>

## Table of Contents

- [Prerequisites](#prerequisites)
- [Technologies Utilized](#technologies-utilized)
- [Features](#features)
- [Run Locally](#run-locally)
- [Deployment](#deployment)
- [API Endpoints](#api-endpoints)
- [Troubleshooting](#troubleshooting)
- [Project Structure](#project-structure)
- [Sample Data](#sample-data)
- [License](#license)
- [Contact](#contact)

### Prerequisites:<a name="prerequisites"></a>

Before setting up AutoRFP, ensure you have the following installed and configured:

- **[Node.js](https://nodejs.org/)** (v18.x or later)
- **[pnpm](https://pnpm.io/)** (v8.x or later)
- **[Git](https://git-scm.com/)** (for version control)
- **[PostgreSQL](https://www.postgresql.org/)** database (local or cloud)
- **[Supabase Account](https://supabase.com/)** (for authentication)
- **[OpenAI API Account](https://platform.openai.com/)** (with credits)
- **[LlamaCloud Account](https://cloud.llamaindex.ai/)** (optional, but recommended)

### Technologies and Services Utilized: <a name="technologies-utilized"></a>

- **Framework:** <img align="center" alt="Next.js" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/nextjs/nextjs-original.svg"> Next.js 15
- **UI Library:** <img align="center" alt="React.js" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/react/react-original.svg"> React 19
- **Programming Language:** <img align="center" alt="TypeScript" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/typescript/typescript-original.svg"> TypeScript
- **Styling:** <img align="center" alt="Tailwind" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/tailwindcss/tailwindcss-original.svg"> Tailwind CSS & <img align="center" alt="Radix UI" height="20" width="20" src="https://avatars.githubusercontent.com/u/75042455?s=200&v=4"> Radix UI
- **Database & ORM:** <img align="center" alt="PostgreSQL" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/postgresql/postgresql-original.svg"> PostgreSQL & <img align="center" alt="Prisma" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/prisma/prisma-original.svg"> Prisma
- **Authentication:** <img align="center" alt="Supabase" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/supabase/supabase-original.svg"> Supabase Auth
- **AI & ML:** <img align="center" alt="OpenAI" height="25" width="25" src="https://img.icons8.com/?size=100&id=Nts60kQIvGqe&format=png&color=FFFFFF"> OpenAI GPT-4o & LlamaIndex
- **Cloud Indexing:** <img align="center" alt="LlamaCloud" height="25" width="25" src="https://cloud.llamaindex.ai/favicon.ico"> LlamaCloud
- **Package Manager:** <img align="center" alt="pnpm" height="25" width="25" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/pnpm/pnpm-original-wordmark.svg"> pnpm

### Features: <a name="features"></a>

- **🤖 AI-Powered Document Processing:** Automatically extract questions and generate contextual responses.
- **📄 Multi-Format Support:** Understands Word, PDF, Excel, and PowerPoint files.
- **🏢 Multi-Tenant Architecture:** Full support for multiple organizations with role-based access control.
- **🤝 Team Collaboration:** Invite team members with different permission levels (owner, admin, member).
- **📂 Project Organization:** Organize RFPs into distinct projects for better management.
- **☁️ LlamaCloud Integration:** Connect seamlessly to LlamaCloud for powerful document indexing.
- **🔍 Advanced Search & Indexing:** Work with multiple document indexes and track sources in responses.
- **💬 Interactive AI Chat:** A modern, chat-style interface for generating and refining responses.
- **✍️ Response Editing:** Easily edit and refine AI-generated responses before finalizing.
- **🔐 Secure Authentication:** Magic Link authentication handled by Supabase Auth.

### Run Locally: <a name="run-locally"></a>

To run **AutoRFP** on your local machine, follow the steps below:

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/RanitDERIA/tata-rfp.git
    ```

2.  **Install Dependencies:**
    ```bash
    pnpm install
    ```

3.  **Environment Setup:**
    Create a `.env.local` file in the root directory and add your configuration:
    ```env
    # Database
    DATABASE_URL="postgresql://username:password@localhost:5432/auto_rfp"
    DIRECT_URL="postgresql://username:password@localhost:5432/auto_rfp"
    
    # Supabase Configuration
    NEXT_PUBLIC_SUPABASE_URL="your-supabase-project-url"
    NEXT_PUBLIC_SUPABASE_ANON_KEY="your-supabase-anon-key"
    
    # OpenAI API
    OPENAI_API_KEY="your-openai-api-key"
    
    # LlamaCloud
    LLAMACLOUD_API_KEY="your-llamacloud-api-key"
    
    # App Configuration
    NEXT_PUBLIC_APP_URL="http://localhost:3000"
    ```

4.  **Database Setup:**
    Set up your local PostgreSQL database and run migrations.
    ```bash
    # Create the database using psql or your preferred tool
    psql -c "CREATE DATABASE auto_rfp;"
    
    # Generate Prisma client
    pnpm prisma generate
    
    # Run migrations
    pnpm prisma migrate deploy
    ```

5.  **Configure Services:**
    - **Supabase:** Create a project and get your URL and Anon Key. Configure authentication providers and email templates.
    - **OpenAI:** Generate an API key and add credits to your account.
    - **LlamaCloud (Optional):** Create a project and generate an API key.

6.  **Start the Development Server:**
    ```bash
    pnpm dev
    ```

7.  **Open Your Browser:**
    Navigate to [http://localhost:3000](http://localhost:3000) to see the application running.

### Deployment: <a name="deployment"></a>

The application is optimized for deployment on **Vercel**, but can be deployed to any platform that supports Node.js.

**Deploy to Vercel:**

1.  Push your code to a GitHub repository.
2.  Connect your repository to Vercel.
3.  Configure the production environment variables in the Vercel project dashboard.
4.  Deploy! Vercel will automatically build and deploy your application.

**Other Deployment Options:**

- Railway
- Heroku
- Digital Ocean App Platform
- AWS Amplify
- Google Cloud Run

### API Endpoints: <a name="api-endpoints"></a>

The application exposes several API endpoints for core functionalities:

-   `POST /api/organizations`: Create a new organization.
-   `POST /api/projects`: Create a new project.
-   `POST /api/extract-questions`: Extract questions from uploaded documents.
-   `POST /api/generate-response`: Generate AI-powered responses.
-   `GET /api/llamacloud/projects`: Get available LlamaCloud projects.
-   `POST /api/llamacloud/connect`: Connect an organization to a LlamaCloud project.

### Troubleshooting: <a name="troubleshooting"></a>

-   **Database Connection Issues:** Ensure your `DATABASE_URL` is correct. You can test the connection with `pnpm prisma db pull`.
-   **Authentication Issues:** Double-check your Supabase URL and keys. Ensure redirect URLs are correctly configured in your Supabase project settings.
-   **AI Processing Issues:** Verify your OpenAI API key has credits. Check your LlamaCloud API key if document indexing fails.
-   **Environment Variables:** Make sure all required variables are set in your `.env.local` file or your deployment platform's settings.

### Project Structure: <a name="project-structure"></a>

```
auto_rfp/
├── app/                          # Next.js 15 App Router
│   ├── api/                      # API routes
│   │   ├── extract-questions/    # Question extraction endpoint
│   │   ├── generate-response/    # Response generation endpoint
│   │   ├── llamacloud/          # LlamaCloud integration APIs
│   │   ├── organizations/       # Organization management APIs
│   │   └── projects/            # Project management APIs
│   ├── auth/                    # Authentication pages
│   ├── login/                   # Login flow
│   ├── organizations/           # Organization management pages
│   ├── projects/                # Project management pages
│   └── upload/                  # Document upload page
├── components/                  # Reusable React components
│   ├── organizations/           # Organization-specific components
│   ├── projects/               # Project-specific components
│   ├── ui/                     # UI component library (shadcn/ui)
│   └── upload/                 # Upload-related components
├── lib/                        # Core libraries and utilities
│   ├── services/               # Business logic services
│   ├── interfaces/             # TypeScript interfaces
│   ├── validators/             # Zod validation schemas
│   ├── utils/                  # Utility functions
│   └── errors/                 # Error handling
├── prisma/                     # Database schema and migrations
├── types/                      # TypeScript type definitions
└── providers/                  # React context providers
```

### Sample Data: <a name="sample-data"></a>

You can test the platform's core features using our sample RFP document. Upload the file to see how questions are automatically extracted. The resultant Excel file shows an example of the structured output the application generates.

#### 🧾 Sample RFP Document: [📥 **Download Sample RFP**](https://github.com/RanitDERIA/tata-rfp/blob/main/Samples/Request%20for%20Proposal%20(RFP)%20-%20TATA%20Power.pdf)

#### 📊 Resultant Excel File: [📥 **Download Resultant Excel File**](https://github.com/RanitDERIA/tata-rfp/blob/main/Samples/Smart%20RFP%20Automation%20Pilot%20-%20Answers.csv)

### License: <a name="license"></a>

This project is licensed under the **MIT License** - see the [LICENSE](LICENSE) file for details.

### Contact: <a name="contact"></a>

If you want to get in touch or have any questions regarding this project, feel free to reach out:

📧 **Email:** bytebardderia@gmail.com
💼 **LinkedIn:** [Ranit Deria](https://www.linkedin.com/in/ranit-deria-916864257/)
🐦 **Twitter:** [@DeriaRanit](https://twitter.com/DeriaRanit)
💻 **GitHub:** [@RanitDERIA](https://github.com/RanitDERIA)

For any inquiries, suggestions, or bug reports, you can also:

- 🐛 Open an issue on GitHub
- 💬 Start a discussion in the repository
- 📩 Send a direct message via social media

---

<div align="center">
  
**⭐ Star this repository if you find it helpful!**

Made with ❤️ by [Ranit Deria](https://github.com/RanitDERIA)

</div>
