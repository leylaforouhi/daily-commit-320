from dataclasses import dataclass


@dataclass
class WorkSession:
    work_minutes: int = 25
    break_minutes: int = 5
    long_break_minutes: int = 15
    sessions_before_long_break: int = 4

    def create_schedule(self, total_sessions):
        if total_sessions < 1:
            raise ValueError("Total sessions must be at least 1")

        schedule = []

        for session in range(1, total_sessions + 1):
            schedule.append(
                f"Session {session}: Work for {self.work_minutes} minutes"
            )

            if session < total_sessions:
                if session % self.sessions_before_long_break == 0:
                    duration = self.long_break_minutes
                    label = "Long break"
                else:
                    duration = self.break_minutes
                    label = "Short break"

                schedule.append(f"{label}: {duration} minutes")

        return schedule


if __name__ == "__main__":
    planner = WorkSession()
    sessions = int(input("How many work sessions? "))

    try:
        for item in planner.create_schedule(sessions):
            print(item)
    except ValueError as error:
        print(f"Error: {error}")
