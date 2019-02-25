# FROM React / Redux class / Epicodus

## scripts.js

*found here https://www.learnhowtoprogram.com/react/redux-716c6ba7-bcca-4d01-97ab-3a0a2723c0aa/structuring-advanced-redux-state*
...
// REDUX REDUCER
const lyricChangeReducer = (state = initialState.songsById, action) => {

  // Declares several variables used below, without yet defining.
  let newArrayPosition;
  let newSongsByIdEntry;
  let newSongsByIdStateSlice;

  switch (action.type) {
    case 'NEXT_LYRIC':

      // Locates the arrayPosition of the song whose ID was provided
      // in the action's payload, and increments it by one:
      newArrayPosition = state[action.currentSongId].arrayPosition + 1;

      // Creates a copy of that song's entry in the songsById state slice,
      // and adds the updated newArrayPosition value we just calculated as its arrayPosition:
      newSongsByIdEntry = Object.assign({}, state[action.currentSongId], {
        arrayPosition: newArrayPosition
      })

      // Creates a copy of the entire songsById state slice, and adds the
      // updated newSongsById state entry we just created to this new copy:
      newSongsByIdStateSlice = Object.assign({}, state, {
        [action.currentSongId]: newSongsByIdEntry
      });

      // Returns the entire newSongsByIdStateSlice we just constructed, which will
      // update state in our Redux store to match this returned value:
      return newSongsByIdStateSlice;

    case 'RESTART_SONG':

      // Creates a copy of the song entry in songsById state slice whose ID matches
      // the currentSongId included with the action, sets the copy's arrayPosition value
      // to 0:
      newSongsByIdEntry = Object.assign({}, state[action.currentSongId], {
        arrayPosition: 0
      })

      // Creates a copy of the entire songsById state slice, and adds the
      // updated newSongsByIdEntry we just created to this copy:
      newSongsByIdStateSlice = Object.assign({}, state, {
        [action.currentSongId]: newSongsByIdEntry
      });

      // Returns the entire newSongsByIdStateSlice we just constructed, which will
      // update the songsById state slice in our Redux store to match the new slice returned:
      return newSongsByIdStateSlice;

      // If action is neither 'NEXT_LYRIC' nor 'RESTART_STATE' type, return existing state:
    default:
      return state;
  }
}
...

*found here https://www.learnhowtoprogram.com/react/redux-716c6ba7-bcca-4d01-97ab-3a0a2723c0aa/combining-reducers*
...
const renderSongs = () => {

  // Retrieves songsById state slice from store:
  const songsById = store.getState().songsById;

  // Cycles through each key in songsById:
  for (const songKey in songsById) {

    // Locates song corresponding with each key, saves as 'song' constant:
    const song = songsById[songKey]

    // Creates <li>, <h3>, and <em> HTMl elements to render this song's
    // information in the DOM:
    const li = document.createElement('li');
    const h3 = document.createElement('h3');
    const em = document.createElement('em');

    // Creates text node containing each song's title:
    const songTitle = document.createTextNode(song.title);

    // Creates text node containing each song's artist:
    const songArtist = document.createTextNode(' by ' + song.artist);

    // Adds songTitle text node to the <em> element we created 3 lines up:
    em.appendChild(songTitle);

    // Adds <em> element that now contains song title to <h3> element created
    // 5 lines up:
    h3.appendChild(em);

    // Also adds songArtist text node created 2 lines up to <h3> element created
    // 6 lines up:
    h3.appendChild(songArtist);

    // Adds click event listener to same  <h3> element, when this <h3> is clicked,
    // an event handler called selectSong() will run, using song's ID as argument:
    h3.addEventListener('click', function() {
      selectSong(song.songId);
    });

    // Adds entire <h3> element to the <li> element created 11 lines above:
    li.appendChild(h3);

    // Appends this <li> element to the <ul> in index.html with a 'songs' ID:
    document.getElementById('songs').appendChild(li);
  }
}

...
