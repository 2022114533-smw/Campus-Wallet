# Campus Wallet - 3단계 두 번째 슬라이스
# 기능: 메뉴 + 거래 입력 + 목록 보기 + CSV 저장/불러오기
# (예산은 다음 단계에서 추가)

import csv  # CSV 파일을 다루는 파이썬 기본 도구

RECORDS_FILE = "records.csv"                       # 거래를 저장할 파일 이름
FIELDS = ["date", "category", "amount", "memo"]    # CSV 칸(열) 이름


def load_data():
    # records.csv 를 읽어 거래 리스트로 만든다. 파일이 없으면 빈 리스트.
    records = []
    try:
        with open(RECORDS_FILE, "r", encoding="utf-8", newline="") as f:
            reader = csv.DictReader(f)             # 각 줄을 딕셔너리로 읽어줌
            for row in reader:
                row["amount"] = int(row["amount"])  # 글자 → 숫자로 변환
                records.append(row)
    except FileNotFoundError:
        pass  # 아직 파일이 없는 첫 실행이면 그냥 빈 리스트로 시작
    return records


def save_data(records):
    # 거래 리스트 전체를 records.csv 에 저장한다.
    with open(RECORDS_FILE, "w", encoding="utf-8", newline="") as f:
        writer = csv.DictWriter(f, fieldnames=FIELDS)
        writer.writeheader()                       # 첫 줄에 칸 이름 쓰기
        for r in records:
            writer.writerow(r)                     # 거래 한 건씩 쓰기


def add_record(records, date, category, amount, memo):
    # 거래 한 건을 딕셔너리로 만들어 리스트에 추가한다
    record = {
        "date": date,
        "category": category,
        "amount": amount,
        "memo": memo,
    }
    records.append(record)


def show_records(records):
    # 저장된 거래를 한 줄씩 보기 좋게 출력한다
    if len(records) == 0:
        print("아직 기록이 없어요.")
        return
    print("----- 거래 목록 -----")
    for r in records:
        print(f"{r['date']} | {r['category']} | {r['amount']}원 | {r['memo']}")


def main():
    records = load_data()   # 프로그램 시작할 때 파일에서 불러오기

    while True:
        print()
        print("===== Campus Wallet =====")
        print("  1. 거래 입력")
        print("  2. 거래 목록 보기")
        print("  3. 종료")
        choice = input("번호를 입력하세요: ")

        if choice == "1":
            date = input("날짜 (예: 2026-05-07): ")
            category = input("카테고리 (예: 식비): ")
            amount = int(input("금액 (수입 +, 지출 -): "))
            memo = input("메모: ")
            add_record(records, date, category, amount, memo)
            save_data(records)          # 추가할 때마다 바로 파일에 저장
            print("저장했어요!")
        elif choice == "2":
            show_records(records)
        elif choice == "3":
            print("안녕히 가세요!")
            break
        else:
            print("1~3 중에서 골라주세요.")


main()
