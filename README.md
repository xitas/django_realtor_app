# Django Realtor App

A Django-powered real estate listing website where visitors can browse properties, search listings, view property details, and send inquiries to realtors. The project also includes user registration, authentication, and a dashboard for viewing a user's submitted inquiries.

## Features

- **Property listings:** Browse published properties, with the newest listings shown first.
- **Property details:** View property information, photos, pricing, and realtor details.
- **Property search:** Filter listings by keyword, city, state, maximum number of bedrooms, and maximum price.
- **Pagination:** Browse property results in pages of six listings.
- **User accounts:** Register, log in, and log out using Django authentication.
- **Inquiry submission:** Send an inquiry about a property; inquiries are saved in the database and an email notification is sent to the realtor.
- **Inquiry history:** Logged-in users can view their submitted inquiries from the dashboard.
- **Realtor profiles:** Store realtor contact information, biographies, photos, and featured-realtor status.
- **Admin panel:** Manage application data through Django's built-in administration interface.
- **Media uploads:** Store property and realtor images.

## Technology Stack

- Python
- Django 4.1.5
- PostgreSQL (`psycopg2`)
- Pillow for image handling
- Django templates and the built-in authentication, admin, and messaging frameworks

## Project Structure

```text
django_realtor_app/
├── accounts/       # Registration, login, logout, and user dashboard
├── btre/           # Django project settings and root URL configuration
├── contacts/       # Property inquiry model and submission handling
├── listings/       # Property model, listing views, search, and pagination
├── pages/          # Home and about pages
├── realtors/       # Realtor model and profile data
├── templates/      # Shared and app-specific HTML templates
├── manage.py
└── requirments.txt # Python dependencies (filename as currently used in the repo)
```

## Requirements

- Python 3.8 or later
- PostgreSQL
- pip

The repository's dependency file pins Django 4.1.5 and the packages listed below. Use a compatible Python version for this older Django release.

## Getting Started

### 1. Clone the repository

```bash
git clone https://github.com/xitas/django_realtor_app.git
cd django_realtor_app
```

### 2. Create and activate a virtual environment

**Windows (PowerShell):**

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

**macOS / Linux:**

```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

The repository currently names its dependency file `requirments.txt` (with the spelling shown here):

```bash
pip install -r requirments.txt
```

### 4. Configure PostgreSQL and Django settings

Create a PostgreSQL database for the application (the current settings use the database name `btredb`).

The checked-in `btre/settings.py` contains development database, email, and Django secret-key settings. **Do not use those values in production or commit real credentials.** Configure your own local overrides in `btre/local_settings.py` (the project settings attempt to import this file when it exists), or update the settings to read secrets from environment variables.

At minimum, configure:

- `SECRET_KEY`
- `DEBUG`
- `ALLOWED_HOSTS`
- `DATABASES`
- Email settings (`EMAIL_HOST`, `EMAIL_PORT`, `EMAIL_HOST_USER`, `EMAIL_HOST_PASSWORD`, and `EMAIL_USE_TLS`)

Make sure the PostgreSQL database and user exist and have the required permissions before running migrations.

### 5. Apply migrations

```bash
python manage.py makemigrations
python manage.py migrate
```

### 6. Create an administrator account

```bash
python manage.py createsuperuser
```

### 7. Run the development server

```bash
python manage.py runserver
```

Open [http://127.0.0.1:8000/](http://127.0.0.1:8000/) in your browser.

The Django admin interface is available at [http://127.0.0.1:8000/admin/](http://127.0.0.1:8000/admin/).

## Application URLs

| URL | Purpose |
|---|---|
| `/` | Home page |
| `/about/` | About page and realtor information |
| `/listings/` | Property listing page |
| `/listings/search` | Property search |
| `/listings/<listing_id>` | Individual property details |
| `/accounts/register/` | User registration |
| `/accounts/login/` | User login |
| `/accounts/dashboard/` | Logged-in user's inquiry dashboard |
| `/admin/` | Django administration |

The exact trailing-slash behavior depends on the URL patterns and Django's `APPEND_SLASH` handling.

## Data Models

### Listing

Stores property information including its title, address, city, state, ZIP code, description, price, bedrooms, bathrooms, garage spaces, square footage, lot size, photos, publication status, listing date, and associated realtor.

### Realtor

Stores a realtor's name, photo, description, phone number, email address, featured-realtor flag, and hire date.

### Contact

Stores inquiries submitted for a property, including the listing reference, sender's name, email, phone, message, submission date, and associated user ID when available.

## Notes

- Add property and realtor records through the Django admin interface.
- Property and realtor images are uploaded under the configured media directory.
- Inquiry email delivery requires valid SMTP settings.
- The project is based on the real estate application tutorial by Brad Traversy and has been organized into Django apps.

## Security and Production Checklist

Before deploying this project:

- Replace the development `SECRET_KEY` and remove all hard-coded credentials.
- Set `DEBUG = False` and configure `ALLOWED_HOSTS`.
- Store database and email credentials in environment variables or a secure secret manager.
- Configure HTTPS, secure cookies, and Django's production security settings.
- Configure a production-ready static and media file serving strategy.
- Review inquiry form validation, authorization, and spam protection.
- Run Django's deployment checks:

```bash
python manage.py check --deploy
```

## License

No license is currently specified in this repository. Add a `LICENSE` file if you intend to grant others permission to use, modify, or distribute this project.
