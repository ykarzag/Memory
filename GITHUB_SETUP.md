# מדריך העלאה ל-GitHub ובנייה אוטומטית של APK 🚀

## שלב 1: הכנת המחשב (פעם אחת בלבד)

### התקן Git אם אין לך:
**Windows:**
- הורד מ: https://git-scm.com/download/win
- התקן עם כל ההגדרות ברירת המחדל

**Mac:**
- פתח Terminal והקלד: `git --version`
- אם אין לך, זה יציע להתקין אוטומטית

**Linux:**
```bash
sudo apt-get install git
```

### הגדר את Git (פעם אחת):
```bash
git config --global user.name "השם שלך"
git config --global user.email "המייל שלך"
```

---

## שלב 2: יצירת חשבון GitHub (אם אין לך)

1. גש ל: https://github.com
2. לחץ על **Sign up**
3. מלא פרטים ואמת את המייל

---

## שלב 3: יצירת Repository חדש ב-GitHub

1. **היכנס ל-GitHub** ולחץ על **+** ליד התמונה שלך → **New repository**

2. **מלא את הפרטים:**
   - **Repository name**: `english-memory-game`
   - **Description**: "משחק זיכרון ללימוד אנגלית לאנדרואיד"
   - בחר: **Public** (כדי ש-GitHub Actions יעבוד בחינם)
   - **אל תסמן** שום דבר אחר (no README, no .gitignore, no license)

3. **לחץ על** "Create repository"

---

## שלב 4: העלאה של הקבצים

### דרך א': באמצעות Terminal/Command Line (מומלץ)

1. **פתח Terminal/Command Prompt** והגע לתיקייה שבה הורדת את הקבצים:
```bash
cd /path/to/EnglishMemoryGame
```

2. **אתחל Git repository:**
```bash
git init
```

3. **הוסף את כל הקבצים:**
```bash
git add .
```

4. **צור commit ראשון:**
```bash
git commit -m "Initial commit - English Memory Game"
```

5. **חבר ל-GitHub** (החלף USERNAME בשם המשתמש שלך):
```bash
git remote add origin https://github.com/USERNAME/english-memory-game.git
```

6. **העלה לענן:**
```bash
git branch -M main
git push -u origin main
```

**הזן שם משתמש וסיסמה של GitHub** (או Personal Access Token אם מבקשים)

---

### דרך ב': העלאה דרך הממשק של GitHub (קל יותר!)

1. **בדף ה-Repository החדש**, תראה מסך עם הוראות
2. **גלול למטה עד** "…or create a new repository on the command line"
3. **לחץ על** "uploading an existing file"
4. **גרור את כל הקבצים והתיקיות** (כולל .github) לתיבה
5. **כתוב הודעת commit**: "Initial commit"
6. **לחץ** "Commit changes"

---

## שלב 5: הפעלת GitHub Actions

ברגע שהעלית את הקבצים, GitHub Actions יתחיל לבנות את ה-APK אוטומטית!

### איך לעקוב אחרי הבנייה:

1. **בדף ה-Repository**, לחץ על הטאב **"Actions"** למעלה
2. תראה workflow בשם **"Build Android APK"** שמתחיל לרוץ
3. **לחץ עליו** כדי לראות את ההתקדמות

### זה אמור לקחת כ-3-5 דקות

אתה תראה שלבים:
- ✅ Checkout code
- ✅ Set up JDK 11
- ✅ Grant execute permission for gradlew
- ✅ Build with Gradle
- ✅ Upload APK

---

## שלב 6: הורדת ה-APK

כשהבנייה מסתיימת בהצלחה:

1. **בדף ה-Actions**, לחץ על ה-workflow שהסתיים (יהיה לו ✅ ירוק)
2. **גלול למטה** עד "Artifacts"
3. תראה **"english-memory-game"** - לחץ עליו להורדה
4. **זה יוריד קובץ ZIP** - חלץ אותו
5. בפנים תמצא: **app-debug.apk** - זה ה-APK שלך! 🎉

---

## שלב 7: התקנה על המכשיר

### על מכשיר אנדרואיד:

1. **העבר את app-debug.apk** למכשיר (דרך USB, WhatsApp, Google Drive וכו')
2. **במכשיר, פתח את הקובץ**
3. אם מופיעה אזהרה **"מקור לא ידוע"**:
   - עבור להגדרות
   - אפשר "התקנה ממקורות לא ידועים" לאפליקציה הזו
4. **לחץ "התקן"**
5. **סיימת!** 🎉

---

## עדכון האפליקציה בעתיד

כשתרצה לעשות שינויים:

1. **ערוך את הקבצים** במחשב שלך
2. **העלה את השינויים:**
```bash
git add .
git commit -m "תיאור מה שינית"
git push
```
3. **GitHub Actions יבנה APK חדש אוטומטית!**

---

## פתרון בעיות 🔧

### הבנייה נכשלה? ❌

**לחץ על ה-workflow הכושל** ותראה איפה השגיאה.

שגיאות נפוצות:

1. **"Permission denied on gradlew"**
   - הוסף בסוף הקובץ `.github/workflows/build.yml` את:
   ```yaml
   - name: Make gradlew executable
     run: chmod +x ./gradlew
   ```

2. **"Could not find com.android.tools.build:gradle"**
   - בדוק שיש אינטרנט ושה-repository הוא Public

3. **"Execution failed for task ':app:processDebugResources'"**
   - ודא שכל קבצי ה-XML נמצאים במקום הנכון

### לא רואה את Actions?
- ודא שה-Repository הוא **Public**
- או הפעל GitHub Actions ידנית: Actions → Build Android APK → Run workflow

---

## מבנה הקבצים הסופי שצריך להעלות

```
english-memory-game/
├── .github/
│   └── workflows/
│       └── build.yml                    ⚠️ חשוב מאוד!
├── .gitignore
├── app/
│   ├── build.gradle
│   └── src/
│       └── main/
│           ├── AndroidManifest.xml
│           ├── java/com/example/englishmemory/
│           │   ├── MainActivity.java
│           │   └── GameActivity.java
│           └── res/
│               ├── drawable/
│               │   ├── card_back.xml
│               │   └── card_front.xml
│               ├── layout/
│               │   ├── activity_main.xml
│               │   └── activity_game.xml
│               └── values/
│                   └── strings.xml
├── gradle/
│   └── wrapper/
│       ├── gradle-wrapper.jar           ⚠️ נדרש!
│       └── gradle-wrapper.properties
├── build.gradle
├── settings.gradle
├── gradle.properties
├── gradlew                              ⚠️ נדרש!
└── gradlew.bat                          (אופציונלי, ל-Windows)
```

---

## שאלות נפוצות ❓

**ש: GitHub Actions זה בחינם?**
ת: כן! 2000 דקות בחודש לחשבונות חינמיים (כל בנייה לוקחת ~3 דקות)

**ש: אני חייב להשתמש ב-GitHub?**
ת: לא, אבל זה הכי קל. אפשר גם GitLab CI או Bitbucket Pipelines

**ש: האפליקציה בטוחה?**
ת: כן, הקוד פתוח וגלוי לכולם. אין בו וירוסים או תוכנות זדוניות

**ש: למה זה קובץ "debug" APK?**
ת: זה APK לפיתוח. לפרסום רשמי ב-Play Store צריך "release" APK חתום

---

## זקוק לעזרה נוספת? 💬

- בדוק את ה-README.md לפרטים על האפליקציה עצמה
- בדוק את PROJECT_STRUCTURE.md להבנת מבנה הקבצים
- פתח Issue ב-GitHub אם יש בעיה

**בהצלחה! 🎉 תיהנה מהאפליקציה!**
