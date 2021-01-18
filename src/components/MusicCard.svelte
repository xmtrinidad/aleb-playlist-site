<script>
  import { deleteIcon, editIcon } from '../app-svgs';
  import { createEventDispatcher } from 'svelte';
  export let musicCard;
 
  const dispatch = createEventDispatcher();
 
  function onThumbnailMouseEnter(e, thumbnail) {
   const location = {
     x: e.clientX,
     y: e.clientY
   };
   dispatch('thumbnail-hover', {thumbnail, location});
  }
 
  function onThumbnailMouseLeave(thumbnail) {
   dispatch('thumbnail-leave', thumbnail);
  }
 
  function onEditClick() {
   dispatch('edit-playlist', musicCard);
  }
  
 </script>

 <style>
   .music-card {
  display: flex;
  flex-direction: column-reverse;
  width: 100%;
  box-shadow: 0 3px 6px rgba(0,0,0,0.16), 0 3px 6px rgba(0,0,0,0.23);
  padding: 16px 24px;
  background-color: #fff;
  border-radius: 4px;
  margin-bottom: 16px;
}

.playlist-info {
  display: flex;
  flex-direction: column-reverse;
}

a {
    width: 100%;
    border: none;
    background-color: #7C4DFF;
    color: #fff;
    border-radius: 4px;
    height: 35px;
    margin-top: 10px;
  }

.created-on {
  margin: 8px 0;
}

.thumbnail-preview {
  display: flex;
  align-items: center;
  width: 100%;
}

.thumbnail-preview button {
  padding: 0;
  margin: 0 2px;
}

.thumbnail-preview img {
  max-width: 100%;
  width: 40px;
  height: 40px;
  border-radius: 100%;
}

.actions {
  display: none;
}

@media (min-width: 768px) {
  .music-card {
    align-items: center;
    justify-content: space-between;
    flex-direction: row;
  }

  .playlist-info {
    align-items: center;
    flex-direction: row;
    width: 40%;
  }

  .playlist-info a {
    margin-top: 0;
    margin-right: 24px;
    width: 80px;
  }

  .thumbnail-preview {
    width: 30%;
    margin-left: 40px;
  }

  .created-on {
    margin: 0;
  }

  .actions {
    display: block;
  }
}
 </style>
 
 <div class="music-card">
   <div class="playlist-info">
     <a href="#/player/{musicCard.id}" class="flex-center">View</a>
     <div>
       <p>{musicCard.playlistName}</p>
       <p>{musicCard.songs.length} songs</p>
     </div>
   </div>
   <div class="created-on">
     <p>{musicCard.createdOn}</p>
   </div>
   <div class="thumbnail-preview">
     {#if musicCard.thumbnails.length >= 1}
       {#each musicCard.thumbnails as thumbnail}
         <button 
           on:mouseleave="{onThumbnailMouseLeave}"
           on:mouseenter="{(e) => onThumbnailMouseEnter(e, thumbnail)}" class="img-container flex-center">
           <img src="{thumbnail.src}" alt="{thumbnail.alt}">
         </button>
       {/each}
     {/if}
   </div>
   <div class="actions">
     <button on:click="{onEditClick}">{@html editIcon}</button>
     <button>{@html deleteIcon}</button>
   </div>
 </div>