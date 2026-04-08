# Manoj
code
TOTAL_SEATS = 100

movies = ["Avengers", "Interstellar", "RRR"]
timings = ["10AM", "2PM", "7PM"]

# Price of each movie
prices = {
    "Avengers": 250,
    "Interstellar": 200,
    "RRR": 180
}

# Seats for each movie and timing
seats = {}
for movie in movies:
    seats[movie] = {}
    for time in timings:
        seats[movie][time] = TOTAL_SEATS

bookings = {}

while True:

    print("\n1. Book Ticket")
    print("2. Cancel Ticket")
    print("3. Show Available Seats")
    print("4. Exit")

    choice = input("Enter choice: ")

    if choice == "1":

        print("\nMovies:")
        for i in range(len(movies)):
            print(i+1, movies[i], "- Price:", prices[movies[i]])

        movie_choice = int(input("Select movie: "))
        movie = movies[movie_choice-1]

        print("\nTimings:")
        for i in range(len(timings)):
            print(i+1, timings[i], "Seats:", seats[movie][timings[i]])

        time_choice = int(input("Select timing: "))
        time = timings[time_choice-1]

        num_seats = int(input("Enter seats: "))

        if num_seats > seats[movie][time]:
            print("Not enough seats")

        else:
            seats[movie][time] -= num_seats

            amount = num_seats * prices[movie]

            booking_id = len(bookings) + 1

            bookings[booking_id] = {
                "movie": movie,
                "time": time,
                "seats": num_seats
            }

            print("\nBooking Successful")
            print("Booking ID:", booking_id)

            print("\n--- BILL ---")
            print("Movie:", movie)
            print("Time:", time)
            print("Price per ticket:", prices[movie])
            print("Seats:", num_seats)
            print("Total:", amount)

    elif choice == "2":

        booking_id = int(input("Enter booking ID: "))

        if booking_id in bookings:

            confirm = input("Confirm cancel (yes/no): ")

            if confirm.lower() == "yes":

                movie = bookings[booking_id]["movie"]
                time = bookings[booking_id]["time"]
                num_seats = bookings[booking_id]["seats"]

                seats[movie][time] += num_seats
                del bookings[booking_id]

                print("Booking Cancelled")

        else:
            print("Invalid Booking ID")

    elif choice == "3":

        for movie in seats:
            print("\n", movie)
            for time in seats[movie]:
                print(time, ":", seats[movie][time])

    elif choice == "4":
        break

    else:
        print("Invalid choice")
