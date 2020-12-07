Challenge: News Search - Clue 1
---------------------------------


Start by copying the code that does the request from the `giggle_news` view
function into that if statement. Here's a snippet of the results of that:


        elif search_type == 'newssearch':
            context['search_message'] = 'Headlines'
            context['results_count'] = 0

            url ='http://content.guardianapis.com/search?api-key=a938fccc-00e9-41ca-905c-741615da8be1'
            response = requests.get(url)
            news_data = response.json()
            results_list = news_data['response']['results']




Challenge: News Search - Clue 2
---------------------------------

Then, you'll need to incorporate the `results_list` into the context
dictionary.  This goes right after what you did above. Here's an example of how
to do that:

        context['news_results'] = results_list


Challenge: News Search - Clue 3
---------------------------------

Finally, we'll look inside of the news.html file, and copy the HTML tempting we
use from there into our news results, so it will show the news search in an
appealing way:


        {% for item in news_results %}
            <div class="row mb-3">
                <div class="col-md-3 text-right text-muted">
                    <h2>{{ item.sectionName }}</h2>
                </div>
                <div class="col">
                    <a href="{{ item.webUrl }}"> <h1>{{ item.webTitle }}</h1> </a>
                </div>
            </div>
        {% endfor %}


Bonus Challenge: Dates
-----------------------


- Hint: Here's
  into a Python datetime nicely:

        def _fix_guardian_dates(results_list):
            for item in results_list:
                original_date = item['webPublicationDate']
                date_format = "%Y-%m-%dT%H:%M:%SZ"
                converted = datetime.strptime(original_date, date_format)
                item['python_date'] = converted


- Hint: In templating, try using the "date" filter to format a date converted
  into a Python datetime nicely:

        {{ item.python_date|date:"l F jS Y" }}


- Hint: Try using the Django Templating templatetag ifchanged in a for loop to
  give "section headers" for each date:

        {% ifchanged item.python_date|date:"l F jS Y" %}
            <div class="mb-3">
                <hr />
                <h1>{{ item.python_date|date:"l F jS Y" }}</h1>
            </div>
        {% endifchanged %}


Bonus Challenge: Pagination
----------------------------

- Hint: We can use "hidden inputs" and a form to pass along the current 

        <!-- Bonus Challenge: Pagination -->
        <div class="justify-content-center d-flex">
            {% if current_page > 1 %}
                <form>
                    <input type="hidden" name="searchterm" value="{{ search_term }}" />
                    <input type="hidden" name="stype" value="{{ search_type }}" />
                    <input type="hidden" name="page_number" value="{{ previous_page_number }}" />
                    <button class="btn btn-lg btn-primary">&laquo;</button>
                </form>
            {% endif %}

            <button class="btn btn-lg btn-secondary">{{ current_page }}</button>
        </div>

