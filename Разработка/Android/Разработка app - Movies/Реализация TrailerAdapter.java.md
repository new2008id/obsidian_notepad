#java #appMovies 

>[! ] Код на языке `Java`

```java
public class TrailersAdapter extends RecyclerView.Adapter<TrailersAdapter.TrailersViewHolder> {  
    private final String TAG = "TrailerAdapter";  
    private List<Trailer> trailers = new ArrayList<>();  
  
    public void setTrailers(List<Trailer> trailers) {  
        this.trailers = trailers;  
        notifyDataSetChanged();  
    }  
  
    @NonNull  
    @Override    public TrailersViewHolder onCreateViewHolder(@NonNull ViewGroup parent, int viewType) {  
        View view = LayoutInflater  
                .from(parent.getContext())  
                .inflate(R.layout.trailer_item, parent, false);  
        return new TrailersViewHolder(view);  
    }  
  
    @Override  
    public void onBindViewHolder(@NonNull TrailersViewHolder holder, int position) {  
        Log.d(TAG, "onBindViewHolder: " + position);  
        Trailer trailer = trailers.get(position);  
        holder.textViewTrailer.setText(trailer.getName());  
    }  
  
    @Override  
    public int getItemCount() {  
        return trailers.size();  
    }  
  
    public static class TrailersViewHolder extends RecyclerView.ViewHolder {  
        private final TextView textViewTrailer;  
        private final ImageView imageViewPlay;  
  
        public TrailersViewHolder(@NonNull View itemView) {  
            super(itemView);  
            textViewTrailer = itemView.findViewById(R.id.textViewTrailer);  
            imageViewPlay = itemView.findViewById(R.id.imageViewPlay);  
        }  
    }  
}
```