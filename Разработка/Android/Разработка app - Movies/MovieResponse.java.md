#java #appMovies 

>[! ] Код на языке `Java`

```java
public class MovieResponse {  
    @SerializedName("docs")  
    private List<Movie> movies;  
  
    public MovieResponse(List<Movie> movies) {  
        this.movies = movies;  
    }  
  
    public List<Movie> getMovies() {  
        return movies;  
    }  
}
```