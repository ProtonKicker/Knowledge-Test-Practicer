# DMV Written Test Practicer

A desktop application for practicing DMV written tests with intelligent question generation and performance tracking.

![Platform](https://img.shields.io/badge/platform-Windows%2011-blue)
![Python](https://img.shields.io/badge/python-3.8+-green)
![GUI](https://img.shields.io/badge/GUI-PyQt5-orange)

## Features

### 📚 Smart Question Generation
- **Customizable Practice Sets**: Choose the number of questions (5-100)
- **Proportional Mixing**: Control the ratio of official vs. AI-generated questions
- **Weak Area Focus**: Specify topics you want to practice (e.g., "Traffic Signs, Right of Way")
- **Priority System**: Official questions are prioritized over past wrong answers

### 📊 Performance Tracking
- **Historical Accuracy**: Track your overall performance across all practice sessions
- **Session Statistics**: View detailed stats for each practice test
- **Question Analytics**: See how many times you've answered each question correctly/incorrectly
- **Pass/Fail Threshold**: 83% passing score (matches real DMV standards)

### 🖥️ User-Friendly Interface
- **Modern PyQt5 GUI**: Clean, professional interface optimized for Windows 11
- **Split-Screen Layout**: Efficient workspace design
- **Repository Management**: Import/export question databases
- **Answer Toggle**: Show/hide answers when previewing questions

## Installation

### Prerequisites
- Python 3.8 or higher
- Windows 11 (or compatible OS)
- pip (Python package manager)

### Step 1: Install Dependencies

Open PowerShell or Command Prompt in the project directory and run:

```powershell
pip install -r requirements.txt
```

Or simply:

```powershell
pip install PyQt5
```

### Step 2: Run the Application

```powershell
python main.py
```

## Usage Guide

### Main Workspace

The application opens to a split-screen workspace:

#### Left Panel (66% width)
**Upper Section - Question Repository:**
- View all questions in the database
- Toggle "Show Answers" to reveal/hide correct answers
- Import questions from external CSV files
- Export your question database
- Refresh view to see updates

**Lower Section - Statistics:**
- **Overall Statistics**: Historical accuracy, total questions answered, correct/incorrect counts
- **Last Session**: Previous test score, pass/fail result, question count

#### Right Panel (33% width)
**Generate Practice Test:**
- Set number of questions desired
- Adjust official questions proportion (0-100%)
- Adjust past wrong questions proportion (0-100%)
- Enter weak areas (comma-separated topics)
- Click "Generate Practice Test" to begin

### Taking a Practice Test

1. **Configure Your Practice:**
   - Enter desired number of questions
   - Set proportions for official and wrong questions
   - Optionally specify weak areas

2. **Click Generate:**
   - The app will generate questions based on your preferences
   - Loading indicator shows generation progress

3. **Answer Questions:**
   - Scroll through all questions
   - Select your answer for each question using radio buttons
   - All questions are displayed at once

4. **Submit:**
   - Click "Submit Answers" when finished
   - If any questions are unanswered, you'll be prompted to confirm
   - Results display immediately with your score and pass/fail status

5. **Review:**
   - See congratulatory message if you passed (83%+)
   - Get encouragement if you didn't pass
   - Return to main menu to view updated statistics

### Question Priority Logic

When generating questions, the system follows this priority:

1. **Official Questions (mn)**: Highest priority
   - If you request 50% official questions, the system first tries to pull from official sources
   
2. **Past Wrong Questions (nk)**: Second priority
   - Questions you've answered incorrectly before
   - Only used if they don't conflict with official question allocation

3. **Random/Generated Questions**: Fill remaining slots
   - AI-generated questions based on DMV topics
   - Weak areas are considered if specified

**Example:**
- Request: 20 questions, 50% official, 30% wrong
- System attempts: 
  - 10 questions from official set
  - 6 questions from past wrong (that aren't already selected as official)
  - 4 random/generated questions

### Managing Question Repository

#### Import Questions
1. Click "Import" in the repository widget
2. Select a CSV file with question data
3. Questions are merged into your existing repository

#### Export Questions
1. Click "Export" in the repository widget
2. Choose save location
3. Your entire repository is saved to a CSV file

#### CSV Format
If you want to manually create or edit questions, use this format:

```csv
origin,question,options,correct_answer,is_official,times_right,times_wrong
"DMV Official","What does a red traffic light mean?","['Stop', 'Go', 'Caution', 'Yield']","Stop",True,5,2
"AI Generated","When parking uphill, turn wheels:",["Toward curb", "Away from curb", "Straight", "Doesn't matter"],"Away from curb",False,3,1
```

## Project Structure

```
DMV Written Test Practicer/
├── main.py                 # Application entry point
├── backend/
│   ├── question_repo.py    # CSV repository management
│   ├── question_generator.py # Smart question generation
│   └── stats_calculator.py # Statistics calculations
├── frontend/
│   ├── main_window.py      # Main application window
│   ├── repo_widget.py      # Repository display widget
│   ├── stats_widget.py     # Statistics display widget
│   ├── generate_widget.py  # Practice generation form
│   └── practice_page.py    # Practice test interface
├── utils/
│   └── constants.py        # Application constants
├── data/
│   ├── question_repo.csv   # Your question database
│   └── practice_log.csv    # Practice session history
├── California Driver's Handbook.pdf  # Official CA DMV handbook (source: https://www.dmv.ca.gov/portal/file/california-driver-handbook-pdf/)
└── requirements.txt        # Python dependencies
```

## Customization

### Adding Your Own Questions

You can add questions in several ways:

1. **Manual CSV Entry**: Edit `data/question_repo.csv` directly
2. **Import Feature**: Use the GUI import function
3. **Practice Logging**: Questions are automatically added when you answer them during practice

### Changing Passing Score

Edit `utils/constants.py`:

```python
PASSING_SCORE = 83  # Change this value
```

### Modifying Default Values

In `utils/constants.py`:

```python
DEFAULT_VALUES = {
    'num_questions': 20,      # Default number of questions
    'official_proportion': 50, # Default official %
    'wrong_proportion': 30,    # Default wrong %
}
```

## Troubleshooting

### Application Won't Start
- Ensure Python 3.8+ is installed
- Verify PyQt5 is installed: `pip install PyQt5`
- Check that all project files are present

### No Questions Available Error
- The question repository is empty by default
- Add questions manually or import a repository
- Download official DMV practice questions and convert to CSV format

### Display Issues on High DPI Screens
- The app includes High DPI scaling
- For older systems, adjust Windows DPI settings

## Tips for Success

1. **Start Small**: Begin with 10-15 question practice sets
2. **Focus on Weak Areas**: Use the weak areas input to target specific topics
3. **Review Mistakes**: Toggle "Show Answers" in repository to study
4. **Track Progress**: Monitor your historical accuracy improvement
5. **Mix Question Types**: Use varying proportions of official and generated questions
6. **Simulate Real Test**: Practice with 25-50 questions to build endurance

## Future Enhancements

- [ ] Support for images in questions (traffic signs)
- [ ] Multiple user profiles
- [ ] Spaced repetition algorithm
- [ ] Mobile version
- [ ] Cloud sync for question repository
- [ ] More DMV state-specific content

## License

This project is provided as-is for educational purposes.

## Support

For issues or questions about the application, please check the documentation or review the code comments for detailed implementation details.

---

**Good luck with your DMV written test preparation! 🚗📝**
