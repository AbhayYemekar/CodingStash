# CodingStash
import sqlite3
from sqlite3 import Error


def create_connection(db_file):
    """ create a database connection to the SQLite database
        specified by the db_file
    :param db_file: database file
    :return: Connection object or None
    """
    conn = None
    try:
        conn = sqlite3.connect(db_file)
    except Error as e:
        print(e)

    return conn


def select_all_movies(conn):

    cur = conn.cursor()
    cur.execute("SELECT * FROM movies")

    rows = cur.fetchall()

    for row in rows:
        print(row)


def select_movies_by_IronMan(conn, IronMan):

    cur = conn.cursor()
    cur.execute("SELECT * FROM movies WHERE IronMan=?", (IronMan,))

    rows = cur.fetchall()

    for row in rows:
        print(row)


def main():
    database = r"C:\Users\DELL\sqlite\db\MoviesDB"

    # create a database connection
    conn = create_connection(database)
    with conn:
        print("1. Query movies by IronMan:")
        select_task_by_IronMan(conn, 1)

        print("2. Query all Movies")
        select_all_movies(conn)


if __name__ == '__main__':
    main()
