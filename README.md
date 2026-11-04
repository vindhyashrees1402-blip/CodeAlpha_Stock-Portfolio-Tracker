# CodeAlpha_Stock-Portfolio-Tracker


def stock_portfolio_tracker():
    # Hardcoded dictionary defining stock prices
    stock_prices = {
        "AAPL": 180,
        "TSLA": 250,
        "GOOGL": 140,
        "MSFT": 400,
        "AMZN": 175
    }

    portfolio = {}
    print("Available stocks and prices per share:")
    for stock, price in stock_prices.items():
        print(f"  {stock}: ${price}")

    print("\nEnter your portfolio details (Type 'done' when finished):")
    
    while True:
        stock_name = input("Enter stock symbol (e.g., AAPL): ").upper()
        if stock_name == 'DONE':
            break
        if stock_name not in stock_prices:
            print("Stock not found in price list. Please choose from available stocks.")
            continue

        try:
            quantity = int(input(f"Enter quantity for {stock_name}: "))
            if quantity < 0:
                print("Quantity cannot be negative.")
                continue
            portfolio[stock_name] = portfolio.get(stock_name, 0) + quantity
        except ValueError:
            print("Invalid input. Please enter a valid number for quantity.")

    # Calculate total investment
    total_investment = 0
    summary_lines = ["--- Stock Portfolio Summary ---"]
    
    print("\n--- Portfolio Summary ---")
    for stock, qty in portfolio.items():
        price = stock_prices[stock]
        value = price * qty
        total_investment += value
        line = f"{stock}: {qty} shares @ ${price} = ${value}"
        print(line)
        summary_lines.append(line)

    total_line = f"\nTotal Investment Value: ${total_investment}"
    print(total_line)
    summary_lines.append(total_line)

    # Optional file saving
    save_option = input("\nWould you like to save this summary to a .txt file? (y/n): ").lower()
    if save_option == 'y':
        filename = "portfolio_summary.txt"
        with open(filename, "w") as file:
            file.write("\n".join(summary_lines))
        print(f"Portfolio successfully saved to {filename}!")

if __name__ == "__main__":
    stock_portfolio_tracker()
