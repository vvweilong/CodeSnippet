    
    private ArrayList<E> datalist;
    private Context context;
    
    public __placeholder__(ArrayList<FileScanner.FilePype> datalist, Context context) {
        this.datalist = datalist;
        this.context = context;
    }

    @Override
    public MyViewHolder onCreateViewHolder(ViewGroup parent, int viewType) {
        TextView textView = new TextView(context);
        return new MyViewHolder(textView);
    }

    @Override
    public void onBindViewHolder(MyViewHolder holder, final int position) {
        
        if (itemClicklistener != null) {
            holder.itemView.setOnClickListener(new View.OnClickListener() {
                @Override
                public void onClick(View v) {
                    itemClicklistener.onItemClicked(position, datalist.get(position).fileName);
                }
            });
        }
    }

    @Override
    public int getItemCount() {
        return datalist == null ? 0 : datalist.size();
    }

    /**
    *  跟 itemlayout 匹配的 viewholder
    */
    public static class MyViewHolder extends RecyclerView.ViewHolder {

        public MyViewHolder(View itemView) {
            super(itemView);
        }
    }
    
    /**
    *  自定义的 itemclicklistener
    */    
    private RecyclerItemClicklistener itemClicklistener;

    public void setItemClicklistener(RecyclerItemClicklistener itemClicklistener) {
        this.itemClicklistener = itemClicklistener;
    }

    public interface RecyclerItemClicklistener {
        void onItemClicked(int position, String filename);
    }