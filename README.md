# WayGo - Travel Recommendation System

## Overview
WayGo is an intelligent travel recommendation system that helps users discover and plan their travel itineraries using machine learning techniques. The system provides personalized travel recommendations based on user preferences and creates optimized daily rundowns to maximize the travel experience.

## Features
- **Collaborative Filtering**: Personalized place recommendations based on user ratings
- **Intelligent Rundown Generation**: Creates daily itineraries with optimal time allocation
- **Distance Optimization**: Considers proximity between locations to minimize travel time
- **Category-Based Scheduling**: Assigns appropriate time slots based on place categories (Culinary, Nature, Shopping, etc.)

## Technology Stack
- **Python**: Core programming language
- **TensorFlow/Keras**: For building and training the recommendation model
- **Pandas**: For data manipulation and analysis
- **GeoPy**: For geographical distance calculations
- **Sastrawi**: For text processing (stemming and stopword removal)
- **Scikit-learn**: For machine learning utilities
- **Matplotlib/Seaborn**: For data visualization

## Dataset
The system uses three main datasets:
1. `user_rating_dataset.xlsx`: Contains user ratings for various places
2. `places_dataset.xlsx`: Contains information about places (name, location, category)
3. `user_id_dataset.xlsx`: Contains user information

## Model Architecture
The collaborative filtering model uses a neural network architecture with embedding layers:
- User Embedding Layer
- User Bias Layer
- Place Embedding Layer
- Place Bias Layer

The model compiles with a binary cross-entropy loss function and Adam optimizer, using RMSE as the evaluation metric.

## How It Works

### Recommendation System
1. **Data Preparation**: Processes user ratings and place data
2. **Model Training**: Trains a neural network to predict user preferences
3. **Recommendation Generation**: Suggests places based on user's past ratings and preferences

### Rundown Generation
1. **Place Selection**: Selects appropriate places from recommendations
2. **Time Allocation**: Assigns places to suitable time slots based on category:
   - 9 PM - 6 AM: Accommodation
   - 6 AM - 8 AM: Culinary (Breakfast)
   - 8 AM - 10 AM: Activity (Nature, Nautical, etc.)
   - 10 AM - 12 PM: Activity 
   - 12 PM - 1 PM: Culinary (Lunch)
   - 1 PM - 3 PM: Activity
   - 3 PM - 5 PM: Activity
   - 5 PM - 7 PM: Culinary (Dinner)
   - 7 PM - 9 PM: Shopping
3. **Distance Optimization**: Minimizes travel distance between consecutive locations

## Usage

### Installation
```bash
# Clone the repository
git clone https://github.com/WayGo12/WayGoApp.git
cd WayGoApp

# Install required packages
pip install -r requirements.txt
```

### Running the System
```python
# Import required modules
import pandas as pd
from model import collaborative_filtering_recommender, recommend_by_collaborative_filtering

# Load data
user_rating_data = pd.read_excel('dataset/user_rating_dataset.xlsx')
places_data = pd.read_excel('dataset/places_dataset.xlsx')
user_data = pd.read_excel('dataset/user_id_dataset.xlsx')

# Train model
model, history, final_accuracy = collaborative_filtering_recommender(
    places_data, 
    user_rating_data, 
    embedding_size=50, 
    batch_size=8, 
    epochs=100, 
    save_model_path='model'
)

# Get recommendations for a specific user
user_id = 12  # Replace with desired user ID
recommendations = recommend_by_collaborative_filtering(model, places_data, user_rating_data, user_id)

# Generate rundown
rundown = generate_rundown_for_user(recommendations)
```

## Model Performance
The model achieves good performance in predicting user preferences, with validation RMSE improving as training progresses. The embedding size of 50 dimensions provides a good balance between model complexity and performance.

## Geographic Coverage
The system currently focuses on Bali, Indonesia with four main regions:
- East Bali (Lat: -8.471148, Long: 115.665717)
- North Bali (Lat: -8.182740, Long: 115.136624)
- West Bali (Lat: -8.409518, Long: 114.979448)
- South Bali (Lat: -8.409518, Long: 115.188916)

## Future Enhancements
- Integration with real-time weather data
- Support for multi-day itineraries
- User feedback integration for continuous improvement
- Mobile application development
- Expansion to other destinations

