# Sabres

Sabres is an ORM library that exposes a [Parse]-like API.

## Quick Start

Create your model by extending [SabresObject].

```java
public class Movie extends SabresObject {
    private static final String TITLE_KEY = "title";
    private static final String YEAR_KEY = "year";

    public String getTitle() {
        return getString(TITLE_KEY);
    }

    public void setTitle(String title) {
        put(TITLE_KEY, title);
    }

    public Short getYear() {
        return getShort(YEAR_KEY);
    }

    public void setYear(Short year) {
        put(YEAR_KEY, year);
    }
```

Initialize Sabres and register your model classes. 

```java
public class MyApplication extends Application {

    @Override
    public void onCreate() {
        super.onCreate();
        SabresObject.registerSubclass(Movie.class);
        Sabres.initialize(this);
    }
```

Create a new Movie object and save it to Sabres:

```java
Movie movie = new Movie();
movie.setTitle("Fight Club");
movie.setYear(1999);
movie.saveInBackground(new SaveCallback() {
    @Override
    public void done(SabresException e) {
        if (e == null) {
            // save was successful
        } else {
            // Save failed 
        }
      }
});
```

Query the Sabres Database with the [SabresQuery] object:

```java
  SabresQuery<Movie> query = SabresQuery.getQuery(Movie.class);
  query.whereEqualTo(TITLE_KEY, title);
  query.findInBackground(new FindCallback<Movie>() {
          @Override
          public void done(List<Movie> objects, SabresException e) {
          if (e == null) {
              if (objects.isEmpty()) {
                  // did not find any objects matching query
              } else {
                  // found some objects
              }
          } else {
              // query failed.
          }
});
```

For a full documentation please see [Wiki].

## Installation

TODO: add gradle link, and a direct jar link.

## License

    Copyright 2015 Tamir Shomer

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

[Wiki]: https://github.com/tamir7/Sabres/wiki
[Parse]: http://www.parse.com
[SabresObject]: https://github.com/tamir7/Sabres/blob/master/sabres/src/main/java/com/sabres/SabresObject.java
[SabresQuery]: https://github.com/tamir7/Sabres/blob/master/sabres/src/main/java/com/sabres/SabresQuery.java
