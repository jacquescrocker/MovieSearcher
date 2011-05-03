# MovieSearcher

MovieSearcher makes it possible to get information about a movie.
It uses IMDB's API that their iPhone applications rely on.

It's build on top of [maddox's](https://github.com/maddox) [imdb-party](https://github.com/maddox/imdb-party) but adds some extra functionality and bugs fixes.

Follow me on [Twitter](http://twitter.com/linusoleander) for more info and updates.

Take a look at [this](https://github.com/oleander/Movies) gem if you want to use [IMDbAPI.com](http://imdbapi.com) instead of [IMDb.com](http://imdb.com/) as source.
 
## What makes this gem so awesome?

MovieSearcher has a really cool feature (*method*) called `find_by_release_name` that makes it possible to search for a movie based on the release name.
You can for example specify ***Heartbreaker 2010 LIMITED DVDRip XviD-SUBMERGE*** and it will return the not to good [*Heartbreaker*](http://www.imdb.com/title/tt1465487/) by [*Pascal Chaumeil*](http://www.imdb.com/name/nm0154312/)

## So how do I use it?

### Get a movie by its imdb id

```` ruby
movie = MovieSearcher.find_movie_by_id("tt0468569")
movie.title 
# => "The Dark Knight"
movie.rating 
# => 8.9
movie.certification 
# => "PG-13"
````

### Find a movie based on the release name
    
```` ruby
MovieSearcher.find_by_release_name("Heartbreaker 2010 LIMITED DVDRip XviD-SUBMERGE").imdb_id 
# => tt1465487
````
  
### Find a movie based on a folder

```` ruby  
MovieSearcher.find_by_folder('~/Downloads/Its.Kind.of.a.Funny.Story.2010.DVDRip.XviD-AMIABLE')
# => #<ImdbParty::Movie:0x10198a060 ... >
````

### Find a movie based on a file containing and imdb link
  
This method does not take any folder that starts with tilde **~** sign.
  
```` ruby
MovieSearcher.find_by_file('/Users/linus/Downloads/Its.Kind.of.a.Funny.Story.2010.DVDRip.XviD-AMIABLE/its.kind.of.a.funny.story.2010.dvdrip.xvid-amiable.nfo')
# => #<ImdbParty::Movie:0x10198a060 ... >
````

### Find a movie based on a downloaded thingy (folder or file)

This method takes anything that you have download and tries to figure out what movie you're talking about.
If a folder is passed it will list all text files in the folder and try to find an imdb link.
If no link or no files are found, it will fall back on the name of the folder.

```` ruby    
MovieSearcher.find_by_download('/Users/linus/Downloads/some_thing_unknown')
# => #<ImdbParty::Movie:0x10198a060 ... >
````

### Find the top 250 movies of all time

```` ruby
MovieSearcher.top_250 
# => [#<ImdbParty::Movie:0x10178ef68 @imdb_id="tt0111161", @poster_url="http://ia.media-imdb.com/images/M/MV5BMTM2NjEyNzk2OF5BMl5BanBnXkFtZTcwNjcxNjUyMQ@@._V1_.jpg" ... >, ...]
````

### Get the currently popular tv shows

```` ruby
MovieSearcher.popular_shows 
# => [#<ImdbParty::Movie:0x101ff2858 @imdb_id="tt1327801", @poster_url="http://ia.media-imdb.com/images/M/MV5BMTYxMjYxNjQxNl5BMl5BanBnXkFtZTcwNTU5Nzk4Mw@@._V1_.jpg", @year="2009", @title="Glee">, ... ]
````

### Some configure alternatives

You can pass some options to the `find_by_release_name` method to specify how it should behave.

Here is an example.

```` ruby
MovieSearcher.find_by_release_name("Heartbreaker 2010 LIMITED DVDRip XviD-SUBMERGE")
````

## What is being returned?

These are the accessors of `ImdbParty::Movie`, the object being returned from `find_by_release_name` for example.

- **imdb_id** (String) The imdb id of the movie.
- **title** (String) The title of the movie.
- **directors** (Array) Related directors.
- **writers** (Array) Related writers.
- **tagline** (String) The movie tagline.
- **company** (String) Company who made the movie.
- **runtime** (String) The length of the movie, `120 min` for example.
- **rating** (Float) The movie rating, from 0 to 10.
- **poster_url** (String) Movie poster. **Beaware**, this image might expire. Use [tmdb_party](https://github.com/jduff/tmdb_party) if you want posters and images.
- **release_date** (Date) The release date of the movie.
- **certification** (String) The certification of the movie, *R* for example.
- **genres** (Array) The most relevant generes for the movie.
- **actors** (Array) Related actors.
- **trailers** (Hash) Related trailers. The key defines the quality of the trailer, like `H.264 480x360` and the value specify the url.

The `actors`, `writers` and `directors` accessors returns an `ImdbParty::Person` object that has the following accessors.

- **imdb_id** (String) The imdb id of the person.
- **role** (String) What role did the actor have in the movie. This is only set when working with an actor.
- **name** (String) The actual name of the actor.

## This sounds supr, how do I help?

- Start by copying the project or make your own branch.
- Navigate to the root path of the project and run `bundle`.
- Start by running all tests using rspec, `rspec spec/movie_searcher_spec.rb`.
- Implement your own code, write some tests, commit and do a pull request.

## Requirements

*MovieSearcher* is tested in OS X 10.6.6, 10.6.7 using Ruby 1.8.7 and 1.9.2

## License

*MovieSearcher* is released under the *MIT license*.