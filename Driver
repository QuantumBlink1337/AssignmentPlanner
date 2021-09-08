import java.util.Scanner;
import java.util.ArrayList;
import java.time.LocalDateTime;
import java.time.format.DateTimeFormatter;

public class MainPlanner {
    // initalize lists to store assignments, subjects, work time, and break time.
    public static ArrayList<String> assignmentList = new ArrayList<String>();
    public static ArrayList<String> subjectList = new ArrayList<String>();
    public static ArrayList<Integer> workTimeList = new ArrayList<Integer>();
    public static ArrayList<Integer> breakTimeList = new ArrayList<Integer>();
    
    public static final double breakMultiplier = 0.34;
    public static int assignmentTime = 0;

    static LocalDateTime rawDate = LocalDateTime.now();
    static DateTimeFormatter formatRubric = DateTimeFormatter.ofPattern("hh:mm a");
    static String currentTime = rawDate.format(formatRubric);

    static Scanner mainScan = new Scanner(System.in);

    public static void main(String[] args) throws InterruptedException {
        timeUpdate();
        // assignmentList.add("Debug"); // enable this to bypass schedule check and go
        // to work method
        boolean firstRun = true;
        boolean commandVerif = false;
        String helpText = "";
        String command = "";
        if (firstRun) {
            if (rawDate.getHour() > 17) {
                System.out.println("Good evening! Ready to work on some assignments?");
            } else if (rawDate.getHour() > 12) {
                System.out.println("Good afternoon! Let's get some work done!");
            } else if (rawDate.getHour() > 6) {
                System.out.println("Good morning! Let's get your day started!");
            } else if (rawDate.getHour() < 6) {
                System.out.println("Boy, you're a night owl! Not complaining though. Let's get some stuff done.");
            }
            firstRun = false;
        }
        if (assignmentList.isEmpty()) {
            helpText = "Looks like you haven't made your schedule yet! You should do that first.";
        }
        System.out.println(helpText);
        while (!commandVerif) {
            command = "";
            System.out.println(
                    "To make your schedule, type \'schedule\'. To work on your assignments, type \'work\'. To view your schedule, type \'view\'. To shut down this program, type \'stop\'.");
            command = stringSuperStrip(mainScan.nextLine());
            if (command.equals("schedule")) {
                if (!assignmentList.isEmpty()) {
                    System.out.println(
                            "Wait, you have an existing schedule already! Type \'confirm\' to go ahead. Type anything else to go back.");
                    command = mainScan.nextLine();
                    if (command.toLowerCase().replaceAll("[^a-zA-Z ]", "").equals("confirm")) {
                        commandVerif = true;
                        assignmentCreator();
                    }
                } else {
                    commandVerif = true;
                    assignmentCreator();
                }
            }
            if (command.equals("work")) {
                if (assignmentList.isEmpty()) {
                    System.out.println("You don't have any assignments planned!");
                } else {
                    commandVerif = true;
                    dayToDay();
                }
            }
            if (command.equals("view")) {
                if (assignmentList.isEmpty()) {
                    System.out.println("You don't have any assignments planned!");
                } else {
                    commandVerif = true;
                    scheduleView();
                }
            }
            if (command.equals("stop")) {
                System.out.println("Are you sure you want to shut down this program? Type \'yes\' or \'no\'.");
                command = mainScan.nextLine();
                if (command.equals("yes"))
                    System.exit(0);
            }
            commandVerif = false;
        }

    }

    public static String stringSuperStrip(String input) {
        input = input.toLowerCase().replaceAll("[^a-zA-Z ]", "");
        return input;
        
    }   
    public static void timeUpdate() {
        rawDate = LocalDateTime.now();
        formatRubric = DateTimeFormatter.ofPattern("hh:mm a");
        currentTime = rawDate.format(formatRubric);
        
    }
    public static void assignmentCreator() throws InterruptedException {
        assignmentList.clear();
        subjectList.clear();
        workTimeList.clear();
        breakTimeList.clear();
        boolean intVerification = false;
        String helpText = "";
        String timeText = "Fantastic! For how long would you like to work on this assignment today?";
        int assignmentCount = 0;
        System.out.println("How many assignments do you have to do today? Note: You don't have to do them all today.");
        while (!intVerification) {
            try {
                assignmentCount = mainScan.nextInt();
                intVerification = true;
                }
            catch(Exception e) {
                    System.out.println(e);
                }
            finally {
                mainScan.nextLine();
            }
         }
        for (int i = 0; i <= assignmentCount - 1; i++) {
            helpText = "";
            intVerification = false;
            System.out.println("Assignment " + (i + 1));
            Thread.sleep(1000);
            System.out.println("What's the name of your assignment?");
            assignmentList.add(mainScan.nextLine());
            // if (assignmentList.get(i).substring(-1).equals(" ")) {
            //     assignmentList.set(i, assignmentList.get(i).substring(0, -1));
            // }
            if (assignmentList.get(i).toLowerCase().contains("essay")) {
                helpText = "Looks like this is an essay you're working on. Remember to pace yourself with this, and avoid doing it all in one go.";
            }
            if (assignmentList.get(i).toLowerCase().contains("project")) {
                helpText = "This is a project of some sort, so don't do it all in one go!";
            }
            System.out.println("Awesome! Now what kind of subject is this?");
            subjectList.add(mainScan.nextLine());
            if (helpText.equals("")) {
                System.out.println(timeText);
            }
            else {
                System.out.println(timeText);
                System.out.println(helpText);
            }
            while (!intVerification) {
                try {
                    workTimeList.add(mainScan.nextInt());
                    intVerification = true;
                    }
                catch(Exception e) {
                        System.out.println("Oops! That's not a time.");
                    }
                finally {
                    mainScan.nextLine();
                    Thread.sleep(2000);
                }
             }
        }
        //mainScan.close();
        breakCalculator();
        System.out.println("You're all done planning your day!");
        Thread.sleep(1000);
        System.out.println("Now returning to Main Menu.");
        Thread.sleep(1000);
    }
    public static void breakCalculator() {
        for (int z : workTimeList) {
            double i = (double) z *breakMultiplier;
            breakTimeList.add((int) i);
        }

    }
    public static String endOfDayCalc () {
        int time = 0;
        for (int x : workTimeList) {
            time = time + x;
        }
        for (int x : breakTimeList) {
            time = time + x;
        }
        LocalDateTime endOfDay = LocalDateTime.now().plusMinutes(time);
        return endOfDay.format(formatRubric);
    }
    public static void dayToDay() throws InterruptedException {
        String rewardMessage = "";
        boolean commandVerif = false;
        String command = "";
        System.out.println("Ready to start working? Based on your course work for the day, your workday should end at " + endOfDayCalc() + " assuming you take the appropriate amount of time for breaks and assignments.");
        Thread.sleep(5000);
        for (int i = 0; i < assignmentList.size(); i++) {
            command = "";
            commandVerif = false;
            if (workTimeList.get(i) >= 40) {
                System.out.println("Looks like you've got a big " + subjectList.get(i) + " assignment that you said was called " + assignmentList.get(i) + ".");
                rewardMessage = "That was a big chunk of your day done!";
            }
            else if (workTimeList.get(i) >= 20) {
                System.out.println("Well, this " + subjectList.get(i) + " assignment is medium sized. You called it " + assignmentList.get(i) +" .");
                rewardMessage = "A medium chunk of your day taken care of.";

            }
            else if (workTimeList.get(i) >= 5) {
                System.out.println("This " + subjectList.get(i) + " assigmment doesn't seem too bad! You called it " + assignmentList.get(i) + " .");
                rewardMessage = "It may be small, but it had a big impact!";

            }
            else {
                System.out.println("You have a(n) " + subjectList.get(i) +" assignment.");
            }
            Thread.sleep(1000);
            System.out.println("Afterwards, you'll get a " + breakTimeList.get(i) + " minute break. Now, let's get to it!");
            Thread.sleep(1000);
            while (!commandVerif) {
                System.out.println("Type \'done\' when you've spent "+ workTimeList.get(i) + " minutes on " + assignmentList.get(i) + " .");
                command = stringSuperStrip(mainScan.nextLine());
                if (command.equals("done")) {
                    commandVerif = true;
                    command = "";
                }
                else if (command.equals("return")) {
                    return;
                }
            }
            commandVerif = false;
            System.out.println(rewardMessage + "  You earned a break. Take " + breakTimeList.get(i) + " minutes to rest. Consider a mindful practice.");
            while (!commandVerif) {
                System.out.println("Type \'done\' when you have finished your break");
                command = mainScan.nextLine();
                if (stringSuperStrip(command).equals("done")) {
                    commandVerif = true;
                    command = "";
                }
            }
            workTimeList.set(i,0);
            breakCalculator();
            System.out.println("Your new end of day is " + endOfDayCalc() + " .");
            
           
            Thread.sleep(4000);
            System.out.println(assignmentList.size());
        }
        System.out.println("Looks like your day is done! Great work!");
    }
    public static void scheduleView() throws InterruptedException {
        String workTime = "";
        for (int i = 0; i < assignmentList.size(); i++) {
            if (workTimeList.get(i) == 0) {
                workTime = "Done!";
            }
            else {
                workTime = Integer.toString(workTimeList.get(i)); 
            }
            System.out.println("Assignment: " + assignmentList.get(i) + " | Subject: " + subjectList.get(i) + " | Work Time: " + workTime);
            
        }
        Thread.sleep(5000);
    }
}
    

 
