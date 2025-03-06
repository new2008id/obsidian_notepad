#java #appMovies 

>[! ] Код на языке `Java`

```java
public class MovieDetailActivity extends AppCompatActivity {  
    private static final String TAG = "MovieDetailActivity";  
    private static final String EXTRA_MOVIE = "movie";  
    private TextView textViewDescription;  
    private TextView textViewYear;  
    private TextView textViewTitle;  
    private ImageView imageViewPoster;  
    private MovieDetailViewModel viewModel;  
    private TrailersAdapter trailersAdapter;  
    private RecyclerView recyclerViewTrailers;  
  
    @Override  
    protected void onCreate(Bundle savedInstanceState) {  
        super.onCreate(savedInstanceState);  
        EdgeToEdge.enable(this);  
        setContentView(R.layout.activity_movie_detail);  
        ViewCompat.setOnApplyWindowInsetsListener(findViewById(R.id.main), (v, insets) -> {  
            Insets systemBars = insets.getInsets(WindowInsetsCompat.Type.systemBars());  
            v.setPadding(systemBars.left, systemBars.top, systemBars.right, systemBars.bottom);  
            return insets;  
        });  
        initViews();  
        trailersAdapter = new TrailersAdapter(); // инициализация адаптера 
        recyclerViewTrailers.setAdapter(trailersAdapter); // установка адаптера 
  
        viewModel = new ViewModelProvider(this).get(MovieDetailViewModel.class);  
        Movie movie = (Movie) getIntent().getSerializableExtra(EXTRA_MOVIE);  
  
        Glide.with(this)  
                .load(movie.getPoster().getUrl())  
                .into(imageViewPoster);  
        textViewTitle.setText(movie.getName());  
        textViewYear.setText(String.valueOf(movie.getYear()));  
        textViewDescription.setText(movie.getDescription());  
  
        viewModel.loadTrailers(movie.getId());  
        viewModel.getTrailers().observe(this, new Observer<List<Trailer>>() {  
  
            @Override  
            public void onChanged(List<Trailer> trailers) {  
                trailersAdapter.setTrailers(trailers); 
                Log.d(TAG, "onChanged: " + trailers.toString());  
            }  
        });  
    }  
  
    private void initViews() {  
        textViewDescription = findViewById(R.id.textViewDescription);  
        textViewYear = findViewById(R.id.textViewYear);  
        textViewTitle = findViewById(R.id.textViewTitle);  
        imageViewPoster = findViewById(R.id.imageViewPoster);  
        recyclerViewTrailers = findViewById(R.id.recyclerViewTrailers);  
    }  
  
    public static Intent newIntent(Context context, Movie movie) {  
        Intent intent = new Intent(context, MovieDetailActivity.class);  
        intent.putExtra(EXTRA_MOVIE, movie);  
        return intent;  
    }  
}
```

>[!warning ] В момент нажатия на фильм, происходит `подгрузка` трейлеров - `trailersAdapter.setTrailers(trailers);`