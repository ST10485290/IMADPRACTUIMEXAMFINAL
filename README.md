# IMADPRACTUIMEXAMFINAL
This is a simple app Andriod app built with kotlin that allows users to managea music playlidst.
The app lets users add songs with details such as title, artist, name, rating and comments, and view a list of all added songs along with the ratings.
The Idea behind the PlaylistManagerApp was inspired by common features found in major music applications such as Spotify, Apple Music, and YouTube Music — where users create and manage personal playlists.
However, this app takes a lightweight and educational approach
•	Instead of streaming real songs, users manually add song information
•	Ratings and comments allow personal tracking, like “liking” or reviewing music
•	Everything is stored locally in memory (no database or login required)
•	It’s a great beginner project to understand arrays, UI, activity navigation, and user input handling in Android
Used TEXTVIEW , BUTTON AND DIFFERNT FONTS TO MAKE IT USER FRIENDLY.

Andriod studio , kotlin language and azure labs were used.

codes.
MAIN ACTIVITY CODE.
package com.yourname.playlistmanagerapp

import android.content.Intent
import android.os.Bundle
import android.widget.*
import androidx.appcompat.app.AppCompatActivity

// Global arrays to store playlist data
val songTitles = arrayListOf<String>()
val artistNames = arrayListOf<String>()
val ratings = arrayListOf<Int>()
val comments = arrayListOf<String>()

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        val addButton = findViewById<Button>(R.id.btnAdd)
        val viewButton = findViewById<Button>(R.id.btnViewDetails)
        val exitButton = findViewById<Button>(R.id.btnExit)

        addButton.setOnClickListener {
            val dialogView = layoutInflater.inflate(R.layout.dialog_add_song, null)
            val dialog = android.app.AlertDialog.Builder(this)
                .setTitle("Add Song to Playlist")
                .setView(dialogView)
                .setPositiveButton("Add") { _, _ ->
                    val title = dialogView.findViewById<EditText>(R.id.editSongTitle).text.toString()
                    val artist = dialogView.findViewById<EditText>(R.id.editArtistName).text.toString()
                    val rating = dialogView.findViewById<EditText>(R.id.editRating).text.toString().toIntOrNull() ?: 0
                    val comment = dialogView.findViewById<EditText>(R.id.editComment).text.toString()

                    if (title.isNotEmpty() && artist.isNotEmpty() && rating in 1..5) {
                        songTitles.add(title)
                        artistNames.add(artist)
                        ratings.add(rating)
                        comments.add(comment)
                        Toast.makeText(this, "Song added successfully!", Toast.LENGTH_SHORT).show()
                    } else {
                        Toast.makeText(this, "Invalid input. Try again.", Toast.LENGTH_SHORT).show()
                    }
                }
                .setNegativeButton("Cancel", null)
                .create()
            dialog.show()
        }

        viewButton.setOnClickListener {
            val intent = Intent(this, DetailsActivity::class.java)
            startActivity(intent)
        }

        exitButton.setOnClickListener {
            finish()
        }
    }
}


DETAILS CODE.
package com.yourname.playlistmanagerapp

import android.os.Bundle
import android.widget.*
import androidx.appcompat.app.AppCompatActivity

class DetailsActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_details)

        val listButton = findViewById<Button>(R.id.btnShowList)
        val avgButton = findViewById<Button>(R.id.btnShowAverage)
        val backButton = findViewById<Button>(R.id.btnBackToMain)
        val resultView = findViewById<TextView>(R.id.txtResult)

        listButton.setOnClickListener {
            val builder = StringBuilder()
            for (i in songTitles.indices) {
                builder.append("${songTitles[i]} - ${artistNames[i]} (Rating: ${ratings[i]}, Comment: ${comments[i]})\\n")
            }
            resultView.text = builder.toString()
        }

        avgButton.setOnClickListener {
            if (ratings.isNotEmpty()) {
                val average = ratings.sum().toDouble() / ratings.size
                resultView.text = "Average Rating: %.2f".format(average)
            } else {
                resultView.text = "No songs to calculate."
            }
        }

        backButton.setOnClickListener {
            finish()
        }
    }
}


DETAILS CODE.
package com.yourname.playlistmanagerapp

import android.os.Bundle
import android.widget.*
import androidx.appcompat.app.AppCompatActivity

class DetailsActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_details)

        val listButton = findViewById<Button>(R.id.btnShowList)
        val avgButton = findViewById<Button>(R.id.btnShowAverage)
        val backButton = findViewById<Button>(R.id.btnBackToMain)
        val resultView = findViewById<TextView>(R.id.txtResult)

        listButton.setOnClickListener {
            val builder = StringBuilder()
            for (i in songTitles.indices) {
                builder.append("${songTitles[i]} - ${artistNames[i]} (Rating: ${ratings[i]}, Comment: ${comments[i]})\\n")
            }
            resultView.text = builder.toString()
        }

        avgButton.setOnClickListener {
            if (ratings.isNotEmpty()) {
                val average = ratings.sum().toDouble() / ratings.size
                resultView.text = "Average Rating: %.2f".format(average)
            } else {
                resultView.text = "No songs to calculate."
            }
        }

ACTIVITY XML
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:orientation="vertical"
    android:padding="24dp"
    android:gravity="center"
    android:layout_width="match_parent"
    android:layout_height="match_parent">

    <TextView
        android:id="@+id/titleText"
        android:text="🎵 Playlist Manager"
        android:textSize="24sp"
        android:textStyle="bold"
        android:layout_marginBottom="24dp"
        android:layout_width="wrap_content"
        android:layout_height="wrap_content" />

    <Button
        android:id="@+id/btnAdd"
        android:text="Add to Playlist"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp" />

    <Button
        android:id="@+id/btnViewDetails"
        android:text="View Playlist Details"
        android:layout_width="match_parent"
        android:layout_height="wrap_content"
        android:layout_marginBottom="16dp" />

    <Button
        android:id="@+id/btnExit"
        android:text="Exit App"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />
</LinearLayout>
        backButton.setOnClickListener {
            finish()
        }
    }
}

