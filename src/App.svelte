<script>
    import Header from './UI/Header.svelte';
    import MeetupGrid from './Meetups/MeetupGrid.svelte';
    import TextInput from './UI/TextInput.svelte';
    import Button from './UI/Button.svelte';
    import EditMeetup from './Meetups/EditMeetup.svelte';

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle:'learning some damm code',
            description: 'In this meetup, we will have some experts to help you',
            imageUrl: 'http://cincinnatifamilymagazine.com/wp-content/uploads/2014/12/Kids-Codking.jpg',
            address: '27th Nerd Rd, 32546 NY',
            contactEmail: 'code@test.com',
            isFavorite: false
        },
        {
            id: 'm2',
            title: 'Swim Together',
            substitle:'doing some fun swim',
            description: 'We will win some meet',
            imageUrl: 'http://en.people.cn/mediafile/201111/20/F201111201006442583612933.jpg',
            address: '28th Swimmer Rd, 32546 NY',
            contactEmail: 'swim@test.com',
            isFavorite: false
        }
    ];

    let editMode; 

    function addMeetup(event) {
        const newMetup = {
            id: Math.random().toString(),
            title: event.detail.title,
            subtitle: event.detail.subtitle,
            description: event.detail.description,
            imageUrl: event.detail.imageUrl,
            contactEmail: event.detail.email,
            address: event.detail.address 
        };

        // meetups.push(newMetup); DOES NOT WORK
        //below works triggered checking with = sign
        meetups = [newMetup,...meetups];
        editMode = null;
    }

    function cancelEdit() {
        editMode = null;
    }

    function toggleFavorite(event) {
        const id = event.detail;
        const updatedMeetup = { ...meetups.find(m => m.id === id)};
        updatedMeetup.isFavorite = !updatedMeetup.isFavorite;
        const meetupIndex = meetups.findIndex(m => m.id === id);
        const updatedMeetups = [...meetups];
        updatedMeetups[meetupIndex] = updatedMeetup;
        meetups = updatedMeetups;
    }
</script>
<style>
    main {
        margin-top: 5rem;
    }

    .meetup-controls {
        margin: 1rem;
    }
</style>

<Header/>

<main>
    <div class="meetup-controls">
        <Button on:click="{() => (editMode='add')}">New Meetup</Button>
    </div>
    
    {#if editMode === 'add'}
        <EditMeetup on:save="{addMeetup}" on:cancel={cancelEdit}/>
    {/if}
    <MeetupGrid {meetups} on:toggleFavorite="{toggleFavorite}"/>
</main>


