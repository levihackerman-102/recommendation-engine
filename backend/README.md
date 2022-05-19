# movie-rec-engine-backend

Here you can find the Movie Recommendation engine backend Flask API code. 

I created this project to leverage the open-source [MovieLens dataset](https://grouplens.org/datasets/movielens/) and hopefully help people figure out what to watch next. Below is an illustration of what the engine will recommend if you enter the movie "Heat (1995)".

![image](https://user-images.githubusercontent.com/26292532/128757396-9f10b632-dbbf-4b7e-a431-cd308cc08c54.png)


## Get started

Next, make sure you have the necessary libraries installed. For example, if you are using anaconda, you can create a separate environment and install necessary libraries as follows:

```
conda create --name py37env python=3.7
conda activate py37env
pip install Flask Flask-Cors pandas
```

**To run the API:**

```
python application.py
```

**To test the API,** in a  separate terminal run the following:

```
curl -X POST http://0.0.0.0:<port>/recms -H 'Content-Type: application/json' -d '{"movie_title":"Heat (1995)"}'
```

If everything is working properly, you should see the following output/recommendations:

![image](https://user-images.githubusercontent.com/26292532/128763468-d0c46790-a393-4e9e-9bdd-daf226d6c105.png)
