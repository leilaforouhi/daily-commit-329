from datetime import date, timedelta


def calculate_savings_goal(
    target_amount,
    current_savings,
    monthly_contribution,
):
    if target_amount < 0 or current_savings < 0:
        raise ValueError("Amounts cannot be negative")

    if monthly_contribution <= 0:
        raise ValueError("Monthly contribution must be positive")

    remaining = max(0, target_amount - current_savings)

    months_needed = (
        (remaining + monthly_contribution - 1)
        // monthly_contribution
    )

    estimated_date = date.today() + timedelta(
        days=months_needed * 30
    )

    return {
        "target": round(target_amount, 2),
        "current_savings": round(current_savings, 2),
        "remaining": round(remaining, 2),
        "months_needed": int(months_needed),
        "estimated_date": estimated_date.isoformat(),
    }


if __name__ == "__main__":
    try:
        target = float(input("Savings target: "))
        current = float(input("Current savings: "))
        monthly = float(input("Monthly contribution: "))

        result = calculate_savings_goal(target, current, monthly)

        print("\nSavings Plan")
        print("-" * 25)

        for key, value in result.items():
            print(f"{key.replace('_', ' ').title()}: {value}")

    except ValueError as error:
        print(f"Invalid input: {error}")
