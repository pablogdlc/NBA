import pandas as pd

def bubble_sort(arr, key):
    n = len(arr)
    for i in range(n):
        for j in range(0, n - i - 1):
            if arr[j][key] < arr[j + 1][key]: # descendente
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

df = pd.read_csv(r'C:\Users\pablo\Downloads\EDA\Nba\games.csv')

df = df.dropna(subset=['PTS_home', 'PTS_away'])

df['TOTAL_POINTS'] = df['PTS_home'] + df['PTS_away']
df['POINT_DIFF'] = abs(df['PTS_home'] - df['PTS_away'])

datos_completos = df.to_dict(orient='records')

sample = datos_completos[:1000]

sorted_by_diff = bubble_sort(sample.copy(), "POINT_DIFF")

print("\n TOP palizas")
for g in sorted_by_diff[:10]:
    print(f"{g['GAME_DATE_EST']}: ID_{int(g['HOME_TEAM_ID'])} {int(g['PTS_home'])} - "
          f"ID_{int(g['VISITOR_TEAM_ID'])} {int(g['PTS_away'])} "
          f"(Diferencia: {int(g['POINT_DIFF'])})")
