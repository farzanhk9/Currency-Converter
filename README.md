import requests

API_URL = "https://api.exchangerate.host/latest"

def convert_currency(amount, from_currency, to_currency):
    response = requests.get(API_URL, params={"base": from_currency, "symbols": to_currency})
    data = response.json()
    if "rates" in data and to_currency in data["rates"]:
        rate = data["rates"][to_currency]
        return amount * rate
    else:
        raise ValueError("Invalid currency code or API error")

def main():
    print("=== CURRENCY CONVERTER ===")
    amount = float(input("Enter amount: "))
    from_currency = input("From currency (e.g. USD, EUR, IRR): ").upper()
    to_currency = input("To currency (e.g. USD, EUR, IRR): ").upper()

    try:
        result = convert_currency(amount, from_currency, to_currency)
        print(f"\n💱 {amount} {from_currency} = {result:.2f} {to_currency}")
    except Exception as e:
        print("⚠️ Error:", e)

if __name__ == "__main__":
    main()
