# Actvst Website - README

## Setup Instructions

This website is built using [Jekyll](https://jekyllrb.com/), a static site generator. Follow these steps to set up and run the project locally.

### Prerequisites
Ensure you have the following installed:
- **Ruby** (Check with `ruby -v`)
- **Bundler** (Install with `gem install bundler`)
- **Jekyll** (Install with `gem install jekyll`)

### Installation
1. Clone the repository:
   ```sh
   git clone https://github.com/bobagold/actvst.git
   cd actvst
   ```
2. Install Dependencies
Run the following command to install the required dependencies:
   ```sh
   bundle install
   ```
3. Run the Jekyll Server
Start a local development server with:
   ```sh
   bundle exec jekyll serve
   ```
4. Open `http://localhost:4000/` in your browser to view the website.

### Deployment Steps
1. Push changes to the `main` (or `gh-pages`) branch.
2. Ensure the repository settings have GitHub Pages enabled under **Settings > Pages**.
3. The site will be automatically built and published by GitHub Pages.

## Firebase Hosting

For additional flexibility, the website can also be hosted on [Firebase Hosting](https://firebase.google.com/docs/hosting).
