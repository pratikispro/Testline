# Quiz Performance Analysis

## Project Overview

This project focuses on analyzing quiz performance based on the provided quiz data and submission history. The goal is to visualize student performance across various topics, identify weak areas where accuracy is low, and generate personalized recommendations to help improve the overall quiz performance. The analysis also includes creating a student persona, summarizing strengths and weaknesses across different quiz topics.

The project fetches JSON data from external APIs, processes it, and presents insightful visualizations such as bar charts, heatmaps, and scatter plots. Additionally, recommendations are generated for students to focus on weak topics based on their historical performance.

## Project Structure

├── main.py # Main script containing data fetching, processing, and visualization logic ├── requirements.txt # List of required Python libraries └── README.md # Project overview, setup instructions, and approach description




### 1. Clone the repository

To get started, clone the repository to your local machine using the following command:

git clone https://github.com/yourusername/quiz-performance-analysis.git
cd quiz-performance-analysis

2. Install required dependencies
Ensure you have Python 3.7+ installed. You can install the necessary Python libraries using pip. The requirements.txt file contains all the necessary libraries for this project.
pip install -r requirements.txt
his will install the following key dependencies:

pandas - Data analysis and manipulation
matplotlib - Data visualization
seaborn - Advanced data visualization
requests - Fetching data from APIs
json - Working with JSON data

3. Run the script
Once the dependencies are installed, you can run the main analysis script (USERPREDICTION.ipynb) to see the results

Approach
1. Data Fetching
The project begins by fetching the quiz data, submission data, and historical performance data from three external URLs using the requests library. The JSON data returned by the APIs is parsed into Python dictionaries, which are then normalized into pandas DataFrames for further processing and analysis.


quiz_data = fetch_json(QUIZ_URL)
submission_data = fetch_json(SUBMISSION_URL)
history_data = fetch_json(HISTORY_URL)
2. Data Normalization
The JSON data is transformed into pandas DataFrames using the json_normalize method. This process allows for easy analysis and manipulation of the data.


quiz_df = pd.json_normalize(quiz_data['quiz']['questions'])
submission_df = pd.json_normalize(submission_data)
history_df = pd.json_normalize(history_data)
3. Performance Analysis
The analyze_historical_performance function groups the historical data by quiz topic and aggregates performance metrics like the number of correct and incorrect answers, total questions attempted, and calculates accuracy for each topic.


performance_summary = history_df.groupby("quiz.topic").agg({
    "correct_answers": "sum",
    "incorrect_answers": "sum",
    "total_questions": "sum"
}).reset_index()
4. Data Visualization
The project generates three main types of visualizations to help understand quiz performance:

Bar Chart for Performance by Topic: A horizontal bar chart displaying accuracy percentages for each quiz topic.
Heatmap of Accuracy by Topic: A heatmap visualizing the accuracy scores across different topics.
Scatter Plot of Correct vs Incorrect Answers: A scatter plot showing the relationship between correct and incorrect answers, with point sizes representing the total number of questions.
These visualizations help identify trends and provide clear insights into performance across different topics.

5. Weak Area Identification and Recommendations
The function find_weak_areas identifies topics where the accuracy is below a given threshold (default 70%). For each weak area, personalized recommendations are generated.


def find_weak_areas(historical_performance, threshold=70):
    weak_topics = historical_performance[historical_performance["accuracy"] < threshold]
    return weak_topics
The recommendations suggest focusing on specific topics to improve accuracy.

6. Student Persona
The define_student_persona function calculates the average accuracy and speed from historical performance data and identifies strong and weak topics. It then generates a "persona" summary that gives an overall picture of the student's strengths and areas for improvement.


def define_student_persona(history_df):
    avg_accuracy = history_df["accuracy"].str.rstrip(" %").astype(float).mean()
    avg_speed = history_df["speed"].astype(float).mean()
    ...


Key Features
Historical Performance Analysis: Visualizes and analyzes quiz performance across different topics.
Weak Area Identification: Detects weak topics where accuracy is below a threshold and suggests improvements.
Student Persona Creation: Summarizes student performance in terms of accuracy, speed, strong topics, and weak topics.
Data Visualization: Includes bar charts, heatmaps, and scatter plots for a more intuitive understanding of the data.
Conclusion
This project provides a comprehensive analysis of quiz performance, identifies areas for improvement, and offers personalized recommendations. The combination of data analysis and visualization makes it an insightful tool for both students and educators.



