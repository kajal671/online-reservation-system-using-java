#Online Reservation System Using Java With Source Code

Introduction:
Welcome to Online Reservation System using Java. This system allows you to make reservations for guests in online mode. Online reservation systems have become increasingly popular in recent years, as more and more businesses look to streamline their booking process and provide a more convenient experience for their customers. In this blog, we will discuss how to build an online reservation system using Java. The online reservation system we will build will be a simple console-based application that allows users to make, view, and cancel reservations. For businesses, online reservation systems offer a number of benefits, including increased efficiency, reduced workload, improved customer experience, and the ability to manage and monitor reservations in real-time. Overall, online reservation systems have become a vital tool for businesses in today’s digital age, providing a streamlined and convenient way for customers to make reservations while helping businesses to operate more efficiently and effectively.

Explanation:
The online reservation system we will build will be a simple console-based application that allows users to make, view, and cancel reservations. We will use the following components to build the system: Reservation Class, Reservation System Class and User Interface. We will discuss about each class and its functionality. Reservation class will represent a reservation and will have properties like name, date, and number of guests. This class consists of methods for name, ID, date etc. ‘this’ keyword is used to get reference of running class. Reservation System class will manage the reservations and will have methods for making a reservation, getting all reservations, getting a reservation by ID, and cancelling a reservation. Array list  has been used in this class to make things simple for adding reservation using ‘add’ function and deleting reservations with ‘remove’ function. User Interface will be a simple console-based interface that allows users to interact with the reservation system. For taking the inputs from user, we have used the scanner class. In while loop all the options have been mentioned as – Make a reservation, view all reservations, Cancel a reservation and Exit. Reservations can simply be made by giving information of user and calling the make reservation method. It will return output as reservation ID. Cancelling of reservation is take place by ID. It will delete reservation of given ID. Summing up all the things, OOPS and some basic java concepts are the core of this system. Happy Coding!

Source Code:
import java.util.*;

class User {
    String username;
    String password;
    List<Reservation> reservations = new ArrayList<>();

    User(String username, String password) {
        this.username = username;
        this.password = password;
    }
}

class Reservation {
    String reservationId;
    String seatNumber;
    String date;
    String destination;

    Reservation(String reservationId, String seatNumber, String date, String destination) {
        this.reservationId = reservationId;
        this.seatNumber = seatNumber;
        this.date = date;
        this.destination = destination;
    }

    @Override
    public String toString() {
        return "Reservation ID: " + reservationId + ", Seat: " + seatNumber +
                ", Date: " + date + ", Destination: " + destination;
    }
}

class ReservationSystem {
    private static final Map<String, User> users = new HashMap<>();
    private static final Scanner scanner = new Scanner(System.in);
    private static User currentUser = null;

    public static void main(String[] args) {
        while (true) {
            System.out.println("\nOnline Reservation System");
            System.out.println("1. Register");
            System.out.println("2. Login");
            System.out.println("3. Exit");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1 -> registerUser();
                case 2 -> loginUser();
                case 3 -> {
                    System.out.println("Exiting...");
                    System.exit(0);
                }
                default -> System.out.println("Invalid option! Try again.");
            }
        }
    }

    private static void registerUser() {
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        if (users.containsKey(username)) {
            System.out.println("Username already exists!");
            return;
        }
        System.out.print("Enter password: ");
        String password = scanner.nextLine();
        users.put(username, new User(username, password));
        System.out.println("Registration successful! Please log in.");
    }

    private static void loginUser() {
        System.out.print("Enter username: ");
        String username = scanner.nextLine();
        System.out.print("Enter password: ");
        String password = scanner.nextLine();

        User user = users.get(username);
        if (user != null && user.password.equals(password)) {
            currentUser = user;
            System.out.println("Login successful!");
            reservationMenu();
        } else {
            System.out.println("Invalid credentials!");
        }
    }

    private static void reservationMenu() {
        while (true) {
            System.out.println("\nReservation Menu");
            System.out.println("1. Book Reservation");
            System.out.println("2. View Reservations");
            System.out.println("3. Cancel Reservation");
            System.out.println("4. Logout");
            System.out.print("Choose an option: ");
            int choice = scanner.nextInt();
            scanner.nextLine();

            switch (choice) {
                case 1 -> bookReservation();
                case 2 -> viewReservations();
                case 3 -> cancelReservation();
                case 4 -> {
                    currentUser = null;
                    System.out.println("Logged out.");
                    return;
                }
                default -> System.out.println("Invalid option! Try again.");
            }
        }
    }

    private static void bookReservation() {
        System.out.print("Enter destination: ");
        String destination = scanner.nextLine();
        System.out.print("Enter date (YYYY-MM-DD): ");
        String date = scanner.nextLine();
        System.out.print("Enter seat number: ");
        String seatNumber = scanner.nextLine();

        String reservationId = UUID.randomUUID().toString();
        Reservation reservation = new Reservation(reservationId, seatNumber, date, destination);
        currentUser.reservations.add(reservation);

        System.out.println("Reservation successful! ID: " + reservationId);
    }

    private static void viewReservations() {
        if (currentUser.reservations.isEmpty()) {
            System.out.println("No reservations found.");
        } else {
            System.out.println("Your Reservations:");
            for (Reservation r : currentUser.reservations) {
                System.out.println(r);
            }
        }
    }

    private static void cancelReservation() {
        System.out.print("Enter Reservation ID to cancel: ");
        String reservationId = scanner.nextLine();

        boolean found = currentUser.reservations.removeIf(r -> r.reservationId.equals(reservationId));

        if (found) {
            System.out.println("Reservation canceled.");
        } else {
            System.out.println("Reservation ID not found!");
        }
    }
}
 How It Works

User Registration: Users can sign up with a username and password.

Login System: Users must log in to access reservation features.

Booking Reservations: Users can book seats by entering the destination, date, and seat number.

Viewing Reservations: Users can see all their reservations.

Canceling Reservations: Users can cancel a booking using the reservation ID.



---

3️⃣ Example Output

Online Reservation System
1. Register
2. Login
3. Exit
Choose an option: 1

Enter username: alice
Enter password: 1234
Registration successful! Please log in.

Choose an option: 2
Enter username: alice
Enter password: 1234
Login successful!

Reservation Menu
1. Book Reservation
2. View Reservations
3. Cancel Reservation
4. Logout
Choose an option: 1

Enter destination: New York
Enter date (YYYY-MM-DD): 2025-02-05
Enter seat number: A12
Reservation successful! ID: 8d5f7c89-5...

Choose an option: 2
Your Reservations:
Reservation ID: 8d5f7c89-5..., Seat: A12, Date: 2025-02-05, Destination: New York

Choose an option: 3
Enter Reservation ID to cancel: 8d5f7c89-5...
Reservation canceled.
