<a id="readme-top"></a>

[![Contributors][contributors-shield]][contributors-url]
[![Forks][forks-shield]][forks-url]
[![Stargazers][stars-shield]][stars-url]
[![Issues][issues-shield]][issues-url]
[![MIT License][license-shield]][license-url]

<br />
<div align="center">
  <h3 align="center">NextMove — Resume Maker</h3>

  <p align="center">
    A full-stack, AI-powered platform for building ATS-friendly resumes with professional templates and in-depth resume analysis.
    <br />
    <a href="https://github.com/Yashrajsinh-Kanchva/nextmove"><strong>Explore the docs »</strong></a>
    <br />
    <br />
    <a href="https://github.com/Yashrajsinh-Kanchva/nextmove/issues/new?labels=bug">Report Bug</a>
    &middot;
    <a href="https://github.com/Yashrajsinh-Kanchva/nextmove/issues/new?labels=enhancement">Request Feature</a>
  </p>
</div>

<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-the-project">About The Project</a>
      <ul>
        <li><a href="#built-with">Built With</a></li>
      </ul>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
        <li><a href="#configuration">Configuration</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#api-endpoints">API Endpoints</a></li>
    <li><a href="#testing">Testing</a></li>
    <li><a href="#troubleshooting">Troubleshooting</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
    <li><a href="#acknowledgments">Acknowledgments</a></li>
  </ol>
</details>

## About The Project

NextMove is a full-stack web application for creating ATS-friendly resumes. It combines a Flask backend, a Streamlit admin panel, and OpenAI GPT integration to help users build professional resumes, get instant ATS compatibility scores, and receive AI-driven improvement suggestions.

Core capabilities:
* Resume Creation — 18+ professional templates, a step-by-step builder, live preview, and PDF export
* AI-Powered Features — AI resume generation, smart scoring, and personalized suggestions via OpenAI GPT
* ATS Analysis — keyword similarity, structure checks, formatting validation, and missing-keyword detection
* User Management — authentication, Google OAuth, password recovery, and a personal dashboard
* Admin Panel — a Streamlit dashboard for managing users, resumes, analytics, and system logs

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Built With

* [![Python][Python.badge]][Python-url]
* [![Flask][Flask.badge]][Flask-url]
* [![MongoDB][MongoDB.badge]][MongoDB-url]
* [![Redis][Redis.badge]][Redis-url]
* [![OpenAI][OpenAI.badge]][OpenAI-url]
* [![Streamlit][Streamlit.badge]][Streamlit-url]
* [![JavaScript][JavaScript.badge]][JavaScript-url]

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Getting Started

Follow these steps to get a local copy of NextMove up and running.

### Prerequisites

* Python 3.8 or later
* MongoDB (local instance or connection string)
* Redis (optional, used for caching and sessions)
* An OpenAI API key (optional, required for AI features)

### Installation

1. Clone the repo
   ```sh
   git clone https://github.com/Yashrajsinh-Kanchva/nextmove.git
   cd nextmove
   ```
2. Create and activate a virtual environment
   ```sh
   # Windows
   python -m venv venv
   venv\Scripts\activate

   # Linux / macOS
   python3 -m venv venv
   source venv/bin/activate
   ```
3. Install dependencies
   ```sh
   pip install -r requirements.txt
   ```
4. Install the spaCy model required for the ATS checker
   ```sh
   python -m spacy download en_core_web_sm
   ```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

### Configuration

Create a `.env` file in the project root:

```env
# Flask
FLASK_ENV=development
SECRET_KEY=your_secret_key_here_min_32_chars

# Database
MONGODB_URI=mongodb://localhost:27017/resume_maker

# Redis (optional)
REDIS_HOST=localhost
REDIS_PORT=6379
REDIS_DB=0

# Google OAuth
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret

# OpenAI (optional — enables AI features)
OPENAI_API_KEY=your_openai_api_key

# Email (optional)
EMAIL_USER=your_email@gmail.com
EMAIL_PASS=your_app_password
```

**MongoDB** — install locally or use MongoDB Atlas, then set `MONGODB_URI`. Default database name is `resume_maker`.

**Redis** — optional; the app runs without it if unavailable.

**OpenAI** — required for the AI resume generator, AI-powered suggestions, and the admin chatbot. Get a key from the [OpenAI platform](https://platform.openai.com/api-keys).

**Google OAuth** — create credentials in the [Google Cloud Console](https://console.cloud.google.com/), enable the relevant API, and set the authorized redirect URI to `http://localhost:5000/api/google/callback`.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Usage

Run the main application:
```sh
python run.py
```

Run the admin panel in a separate terminal:
```sh
streamlit run admin/admin_app.py
```

| Service | URL |
|---|---|
| Main App | `http://localhost:5000` |
| Admin Panel | `http://localhost:8501` |

**Creating a resume:** sign up or sign in with Google, choose a template, fill in personal info, education, and experience, add skills, then preview and export as PDF.

**AI resume generator:** click "Create with AI," enter a job role and description, fill in your details, and let the AI generate a draft resume to review and save.

**ATS score checker:** select a saved resume, paste a job description, and run the check to get an overall score, keyword match percentage, missing keywords, and formatting feedback.

_For more examples, see the full documentation in the repository._

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## API Endpoints

| Endpoint | Description |
|---|---|
| `POST /api/users/signup` | User registration |
| `POST /api/users/login` | User login |
| `GET /api/users/profile` | Get user profile |
| `POST /api/users/logout` | User logout |
| `GET /api/resumes` | Get all user resumes |
| `POST /api/resumes` | Create a new resume |
| `GET /api/resumes/:id` | Get a resume by ID |
| `PUT /api/resumes/:id` | Update a resume |
| `DELETE /api/resumes/:id` | Delete a resume |
| `POST /api/ai-resume/create` | Generate an AI resume |
| `POST /api/ats/check` | Check ATS score from a PDF |
| `POST /api/ats/check-from-resume` | Check ATS score for a saved resume |
| `GET /api/admin/users` | Get all users (admin) |
| `POST /api/admin/users/:id/block` | Block a user (admin) |
| `GET /api/admin/resumes` | Get all resumes (admin) |
| `GET /api/admin/analytics` | Get analytics (admin) |

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Testing

```sh
# Backend tests
python test.py

# OpenAI API integration test
python test_openai.py
```

Manual test checklist: user registration and login, resume creation, PDF download, ATS checker with a sample job description, and the AI resume generator.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Troubleshooting

| Issue | Fix |
|---|---|
| MongoDB connection error | Ensure MongoDB is running and `MONGODB_URI` in `.env` is correct |
| Redis connection error | Redis is optional; verify `REDIS_HOST` / `REDIS_PORT` if you intend to use it |
| spaCy model not found | Run `python -m spacy download en_core_web_sm` |
| OpenAI API errors | Verify the API key, quota, and billing status |
| PDF generation fails | Check the browser console; ensure jsPDF is loaded; try another browser |
| OAuth not working | Verify Google OAuth credentials and that the redirect URI matches exactly |

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Roadmap

- [ ] Multi-language support
- [ ] Resume sharing via link
- [ ] Cover letter generator
- [ ] Resume templates marketplace
- [ ] Advanced analytics dashboard
- [ ] Mobile app (React Native)
- [ ] Integration with job boards
- [ ] Resume versioning system

See the [open issues](https://github.com/Yashrajsinh-Kanchva/nextmove/issues) for a full list of proposed features and known issues.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contributing

Contributions are what make the open source community such an amazing place to learn, inspire, and create. Any contributions you make are greatly appreciated.

1. Fork the Project
2. Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3. Commit your Changes (`git commit -m 'Add: description of your feature'`)
4. Push to the Branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

Code style: use meaningful variable names, add docstrings to functions, follow PEP 8 for Python code, and use 4-space indentation.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## License

Distributed under the MIT License. See `LICENSE` for more information.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Contact

Yashrajsinh Kanchva — [GitHub Profile](https://github.com/Yashrajsinh-Kanchva)

Mihir Rathod — [GitHub Profile](https://github.com/mihir021)

Project Link: [https://github.com/Yashrajsinh-Kanchva/nextmove](https://github.com/Yashrajsinh-Kanchva/nextmove)

<p align="right">(<a href="#readme-top">back to top</a>)</p>

## Acknowledgments

* [OpenAI](https://openai.com/) — GPT API powering the AI features
* [spaCy](https://spacy.io/) — natural language processing
* [scikit-learn](https://scikit-learn.org/) — TF-IDF vectorization and similarity scoring
* [Flask](https://flask.palletsprojects.com/) — web framework
* [MongoDB](https://www.mongodb.com/) — database
* [Streamlit](https://streamlit.io/) — admin dashboard framework

<p align="right">(<a href="#readme-top">back to top</a>)</p>

<!-- MARKDOWN LINKS & IMAGES -->
[contributors-shield]: https://img.shields.io/github/contributors/Yashrajsinh-Kanchva/nextmove.svg?style=for-the-badge
[contributors-url]: https://github.com/Yashrajsinh-Kanchva/nextmove/graphs/contributors
[forks-shield]: https://img.shields.io/github/forks/Yashrajsinh-Kanchva/nextmove.svg?style=for-the-badge
[forks-url]: https://github.com/Yashrajsinh-Kanchva/nextmove/network/members
[stars-shield]: https://img.shields.io/github/stars/Yashrajsinh-Kanchva/nextmove.svg?style=for-the-badge
[stars-url]: https://github.com/Yashrajsinh-Kanchva/nextmove/stargazers
[issues-shield]: https://img.shields.io/github/issues/Yashrajsinh-Kanchva/nextmove.svg?style=for-the-badge
[issues-url]: https://github.com/Yashrajsinh-Kanchva/nextmove/issues
[license-shield]: https://img.shields.io/github/license/Yashrajsinh-Kanchva/nextmove.svg?style=for-the-badge
[license-url]: https://github.com/Yashrajsinh-Kanchva/nextmove/blob/main/LICENSE
[Python.badge]: https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white
[Python-url]: https://www.python.org/
[Flask.badge]: https://img.shields.io/badge/Flask-000000?style=for-the-badge&logo=flask&logoColor=white
[Flask-url]: https://flask.palletsprojects.com/
[MongoDB.badge]: https://img.shields.io/badge/MongoDB-4EA94B?style=for-the-badge&logo=mongodb&logoColor=white
[MongoDB-url]: https://www.mongodb.com/
[Redis.badge]: https://img.shields.io/badge/Redis-DC382D?style=for-the-badge&logo=redis&logoColor=white
[Redis-url]: https://redis.io/
[OpenAI.badge]: https://img.shields.io/badge/OpenAI-412991?style=for-the-badge&logo=openai&logoColor=white
[OpenAI-url]: https://platform.openai.com/
[Streamlit.badge]: https://img.shields.io/badge/Streamlit-FF4B4B?style=for-the-badge&logo=streamlit&logoColor=white
[Streamlit-url]: https://streamlit.io/
[JavaScript.badge]: https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black
[JavaScript-url]: https://developer.mozilla.org/en-US/docs/Web/JavaScript
