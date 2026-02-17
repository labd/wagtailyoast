# Wagtailyoast

[Yoastseo](https://github.com/Yoast/javascript/tree/master/packages/yoastseo) + [Wagtail](https://github.com/wagtail/wagtail) = 🚀

## Features

- SEO analysis and recommendations powered by YoastSEO
- Real-time content analysis in Wagtail admin
- Keyword optimization suggestions
- Readability analysis
- Meta description and title optimization
- Customizable YoastPanel for Wagtail pages

## Compatibility

- Django 5.0+
- Wagtail 7.0+
- YoastSEO 1.80.0

## Installation

### Using pip

```bash
pip install wagtailyoast
```

### Django Configuration

Add the package to your `INSTALLED_APPS`:

```python
# settings.py

INSTALLED_APPS = [
    # ...
    'wagtailyoast',
    # ...
]
```

## Settings

Configure the following settings in your `settings.py`:

```python
# Locale used for Yoast analysis (default: 'en_US')
WY_LOCALE = 'en_US'

# Make sure you have STATIC_URL configured
STATIC_URL = '/static/'
```

## Usage

Add YoastPanel to your Page models:

```python
from wagtail.admin.edit_handlers import TabbedInterface, ObjectList
from wagtailyoast.edit_handlers import YoastPanel

class TestPage(Page):
    # ... your page fields ...
    keywords = models.CharField(default='', blank=True, max_length=100)

    edit_handler = TabbedInterface([
        ObjectList(Page.content_panels, heading='Content'),
        ObjectList(Page.promote_panels, heading='Promotion'),
        ObjectList(Page.settings_panels, heading='Settings'),
        YoastPanel(
            keywords='keywords',
            title='seo_title',
            search_description='search_description',
            slug='slug'
        ),
    ])
```

### YoastPanel Parameters

- `keywords`: Default keywords of the page
- `title`: 'Search Engine Friendly' title that appears at the top of the browser window
- `search_description`: 'Search Engine Friendly' description for search results
- `slug`: URL slug of the page

## Development

To develop on this package:

1. Clone the repository:

```bash
git clone git@github.com:Aleksi44/wagtailyoast.git
cd wagtailyoast
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Set up the database and run migrations:

```bash
python manage.py migrate
python manage.py init
```

4. Start the Django development server:

```bash
python manage.py runserver 0.0.0.0:4243
```

5. In a separate terminal, start the Webpack development server:

```bash
yarn install
yarn start
```

### Local Development Integration

To use this package for development in another Wagtail project, install it as an editable package:

#### Using pip

```bash
pip install -e path/to/wagtailyoast
```

#### Using pdm

```bash
pdm add -e path/to/wagtailyoast
```

#### Using uv

```bash
uv add --editable path/to/wagtailyoast
```

This allows you to make changes to the `wagtailyoast` package and see them immediately reflected in your Wagtail project without needing to reinstall the package.
