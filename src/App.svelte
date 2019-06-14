<script>
    import Header from './UI/Header.svelte';
    import MeetupGrid from './Meetups/MeetupGrid.svelte';
    import TextInput from './UI/TextInput.svelte';
    import Button from './UI/Button.svelte';

    let title='';
    let subtitle = '';
    let address='';
    let email='';
    let description='';
    let imageUrl = '';

    let meetups = [
        {
            id: 'm1',
            title: 'Coding Bootcamp',
            subtitle:'learning some damm code',
            description: 'In this meetup, we will have some experts to help you',
            imageUrl: 'http://cincinnatifamilymagazine.com/wp-content/uploads/2014/12/Kids-Codking.jpg',
            address: '27th Nerd Rd, 32546 NY',
            contactEmail: 'code@test.com'
        },
        {
            id: 'm2',
            title: 'Swim Together',
            substitle:'doing some fun swim',
            description: 'We will win some meet',
            imageUrl: 'http://en.people.cn/mediafile/201111/20/F201111201006442583612933.jpg',
            address: '28th Swimmer Rd, 32546 NY',
            contactEmail: 'swim@test.com'
        }
    ];

    function addMeetup() {
        const newMetup = {
            id: Math.random().toString(),
            title: title,
            subtitle: subtitle,
            description: description,
            imageUrl: imageUrl,
            contactEmail: email,
            address: address
        };

        // meetups.push(newMetup); DOES NOT WORK
        //below works triggered checking with = sign
        meetups = [newMetup,...meetups];
    }
</script>
<style>
    main {
        margin-top: 5rem;
    }
    form {
        width: 30rem;
        max-width: 90%;
        margin: auto;
    }
</style>

<Header/>

<main>
    <form on:submit|preventDefault={addMeetup}>
        <TextInput 
            id="title"
            label="Title"
            value={title}
            type="text"
            on:input={event => (title = event.target.value)} />
        <TextInput 
            id="subtitle"
            label="Subtitle"
            value={subtitle}
            type="text"
            on:input={event => (subtitle = event.target.value)} />
        <TextInput 
            id="address"
            label="Address"
            value={address}
            type="text"
            on:input={event => (address = event.target.value)} />
        <TextInput 
            id="imageUrl"
            label="Image Url"
            value={imageUrl}
            type="text"
            on:input={event => (imageUrl = event.target.value)} />
        <TextInput 
            id="email"
            label="E-Mail"
            value={email}
            type="email"
            on:input={event => (email = event.target.value)} />
        <TextInput 
            id="description"
            label="Description"
            value={description}
            controlType ="textarea"
            on:input={event => (description = event.target.value)} />
        <Button type="submit" caption="Save"/>
    </form>
    <MeetupGrid {meetups}/>
</main>


