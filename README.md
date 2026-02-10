import pandas as pd
import time
def clean_chunk(df):
    for col in df.columns:
        try:
            df[col] = pd.to_numeric(df[col])
        except:
            pass
    return df
def process_large_file(path_in, path_out, chunksize=5000):
    print("جزء المعالجة")
    start = time.time()
    first = True
    for chunk in pd.read_csv(path_in, chunksize=chunksize):
        print("هذا جزء الطباعة")
        print(chunk.head(3))   # هنا يطبع اول ثالثة اسطر تجربة
        chunk = clean_chunk(chunk)
        chunk.to_csv(path_out, mode='a', index=False, header=first)
        first = False
    print("انتهى بناجح ")
    print("كم اخذ وقت:", round(time.time() - start, 2), "ثانية")
process_large_file(
    "C:/Users/hp/Documents/day13_large_users.csv",
    "C:/Users/hp/Documents/day13_large_users_cleaned.csv",
    chunksize=5000)
