This is an involved activity, building a complicated web app! Focus first on
understanding existing code, then work on adding necessary additions.

- NOTE: This activity is throwing you into the deep-end! It's by far the
  largest application we've looked at.

Challenge 1
-----------

Get the code working!

1. Run the following commands:


    pipenv --python 3           # Create a new virtualenv
    pipenv shell                # Enter the virtualenv
    pipenv install django       # Download Django package into virtualenv
    pipenv install requests     # Download requests package into virtualenv
    python manage.py runserver  # Run the Django Python web-server itself

2. Now, visit http://localhost:8000

3. What's the first thing you do with a new Python file? Add a print!

4. Test out the web application, and examine the code.
    - Examine the views.py.
        - Trace how the Giggle News page works, making an API GET request
        - Examine the views.py. Trace how the Giggle News page works.
    - Can you explain in your own words how the existing web application works?
      What's left to be done?
    - Hint: There are clues in the comments in the files.




Challenge 2
-----------

The goal of this challenge is to get more familiar with the Guardian news API,
and have the Giggle News page display 50 results instead of the default.

Visit the following API URL:

        http://content.guardianapis.com/search?api-key=a938fccc-00e9-41ca-905c-741615da8be1

- See the "api-key"? API keys are like a "password" for an API. Many APIs
  require you register and get an API key before you use them, to prevent abuse
  of the API. This is an API key to be shared by students of this course.

- Try adding the text "&page-size=50" to the end of the URL. See how it
  responds with more results? Congrats, you just added a "GET" parameter!
    - GET parameters go in the URL and are separated with the `&` character.
    - They are sent in the request as part of the path
    - APIs often use them sort of like arguments to a function

- Finally, take the new URL you created, and replace the existing URL being
  used for the Giggle News view function with this URL to get more results



The remaining challenges are all about incorporating new APIs into the search
application. They can be done in any order, but you might consider starting
with the News Search.




Challenge: News Search
----------------------

Using the existing Giggle News code as a guide, finish the Google News Search
functionality.

Hints:

- Start by just getting SOMETHING displayed when searching for news articles.
  Worry about including the query after.
- Look at how the Giggle News view function works, and copy code as needed into
  the Giggle Search view function.
- You'll also need to add code to the template -- consider using the same
  formatting you find in the Giggle News page.
- Still stuck? Take a look at the `code_hints.md` file for more hints.




Challenge: Book Search
----------------------

Open Library is an API to look up information on books.

Example API request: http://openlibrary.org/search.json?q=Mockingjay

Using this as a guide, write code to complete the book search functionality.

Hints:

- Start by just getting SOMETHING displayed when searching for books.  Worry
  about including the correct query after.




Challenge: Music Search
----------------------

Musicbrainz is an API to look up info on music artists and albums.

Example API request: http://musicbrainz.org/ws/2/release/?fmt=json&query=cardi+b

Using this as a guide, write code to complete the book search functionality.


Hints:

- Start by just getting SOMETHING displayed when searching for music.  Worry
  about including the correct query after.




Bonus Challenge: Improved Dates
-------------------------------

Currently, when displaying the dates on Giggle News articles, they look cryptic
and hard to read. This is because we are just displaying the date format that
Guardian API uses, which is more for computers than it is for humans.

To fix this, we'll need to write code that will cause Python to convert these
dates into Python "datetime objects". This will let us then format them as we
please.

Hints:

- The Guardian API uses a date-format that can be converted with the following
  code:

    from datetime import datetime
    date_format = "%Y-%m-%dT%H:%M:%SZ"
    datetime.strptime('2008-09-26T01:51:42.000Z', date_format)

- For more examples, check out this Stack Overflow question:
    - <https://stackoverflow.com/questions/214777/>

- Hint: See `code_hints.md` for more clues




Bonus Challenge: Pagination
-------------------------------

This one's super tough! Can you add a pagination feature?  Add links to the
bottom of each page like:

        << 13 >>

Where clicking on one of the arrows will take you the next (or previous page)
of search results.

- Hint: We'll need to use "offset" API GET parameters (for Musicbrainz and Open
  Library APIs) and "page" (for the Guardian News API) to access more pages of
  information

- Hint: See `code_hints.md` for more clues



Bonus Challenge: New API
---------------------------

- Add a new search functionality! This will require repeating similar steps to
  above, but also researching the API and how to use it.

- There are hundreds of free APIs to use. Browse them here:
    - https://github.com/public-apis/public-apis

- Keep in mind when choosing an API, that not all APIs are not created equal:
    - Some may require registration and obtaining an API key
    - Others may be poorly documented, or hard to use

- Suggested ideas APIs:
    - Movie search with OMDB
        - For testing, feel free to use the following API key, shared with all
          students: 187a5752
    - GIF search with Giphy
        - For testing, feel free to use the following API key, shared with all
          students: dc6zaTOxFJmzC

- Note that no solution is provided for this one.
