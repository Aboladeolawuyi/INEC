<template>
    <v-app>

        <v-app-bar app color="#008000">
            <img src="@/views/inec2.jpeg" alt="INEC" @click="toggleDrawer" class="logo" />
            <v-toolbar-title class="white--text">
                INDEPENDENT NATIONAL ELECTORAL COMMISSION (INEC)
            </v-toolbar-title>

            <v-menu>
                <template v-slot:activator="{ props }">
                    <v-btn v-bind="props" icon>
                        <v-icon>mdi-dots-vertical</v-icon>
                    </v-btn>
                </template>
                <v-list>
                    <v-list-item>
                        <v-btn><v-icon>mdi-account</v-icon> A</v-btn>
                    </v-list-item>
                    <v-list-item>
                        <v-btn><v-icon>mdi-logout</v-icon> Logout</v-btn>
                    </v-list-item>
                </v-list>
            </v-menu>
        </v-app-bar>

        <v-main>
            <v-container fluid>
                <router-view></router-view>

                <v-card style="margin:auto;">
                    <v-card-title class="text-center" style="margin: auto; color:white; background-color: green;">ELECTION
                        RESULT PAGE</v-card-title>
                    <v-card-text>
                        <v-btn @click="dialog = true">ADD RESULT</v-btn>
                        <v-btn @click="loadvotes()">
                            LOAD VOTES
                        </v-btn>
                    </v-card-text>
                </v-card>
                <v-card>
                    <v-card-title>
                        ELECTION RESULT
                    </v-card-title>
                    <v-card-text>
                        <v-simple-table>
                            <template v-slot:default>
                                <thead>
                                    <tr>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">S/N</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">RA</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">Code</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">Regd
                                            Voters</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">Accrd
                                            Voters</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">A</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">AAC</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">ADC</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">ADP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">APC</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">APM</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">APP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">BP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">LP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">NNPP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">NRM</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">PDP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">PRP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">SDP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">YPP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">ZLP</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">Total
                                            Valid Votes</th>
                                        <th class="text-left"
                                            style="background-color: green; color: white; border: 1px solid #ccc;">Rejected
                                            Votes</th>
                                    </tr>
                                </thead>
                                <tbody>
                                    <tr v-for="(vote, index) in votes" :key="index">
                                        <td style="border: 1px solid #ccc;">{{ vote.serialNumber }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.nameOfRA }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.code }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.numberOfRegisteredVoters }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.numberOfAccreditedVoters }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.A }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.AAC }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.ADC }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.ADP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.APC }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.APM }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.APP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.BP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.LP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.NNPP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.NRM }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.PDP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.PRP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.SDP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.YPP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.ZLP }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.totalValidVotes }}</td>
                                        <td style="border: 1px solid #ccc;">{{ vote.rejectedVotes }}</td>
                                    </tr>
                                </tbody>
                            </template>
                        </v-simple-table>
                    </v-card-text>
                </v-card>

                <v-dialog v-model="dialog" max-width="800px">
                    <v-card>
                        <v-card-title class="headline">Enter Election Results</v-card-title>
                        <v-card-text>
                            <v-form @submit.prevent="addvotes">
                                <v-container>
                                    <v-row>
                                        <v-col cols="4" v-for="(field, label) in formData" :key="label">
                                            <v-text-field v-model="formData[label]" :label="label"></v-text-field>
                                        </v-col>
                                    </v-row>
                                </v-container>
                            </v-form>
                        </v-card-text>
                        <v-card-actions>
                            <v-btn color="primary" @click="addvotes()">Submit</v-btn>
                            <v-btn color="error" @click="cancel()">Cancel</v-btn>
                        </v-card-actions>
                    </v-card>
                </v-dialog>
            </v-container>
        </v-main>
    </v-app>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            dialog: false,
            votes: [],
            formData: {
                serialNumber: '001',
                nameOfRA: 'Lokoja - A',
                code: '01',
                numberOfRegisteredVoters: '7905',
                numberOfAccreditedVoters: '4134',
                A: '11',
                AAC: '12',
                ADC: '27',
                ADP: '2303',
                APC: '4756',
                APM: '476',
                APP: '11',
                BP: '314',
                LP: '721',
                NNPP: '124',
                NRM: '745',
                PDP: '4756',
                PRP: '32',
                SDP: '752',
                YPP: '759',
                ZLP: '254',
                totalValidVotes: '28467',
                rejectedVotes: '1301',

            },
        };
    },
    methods: {

        loadvotes() {
            axios
                .get('https://localhost:7050/api/votes')
                .then(response => {
                    console.log(response.data)
                    this.votes = response.data;

                })
                .catch(error => {
                    console.error('Error loading data:', error);
                    console.log('VOTES SUBMITTED SUCCESSFULLY:')
                });
        },
        addvotes() {
            axios
                .post('https://localhost:7050/api/votes', this.formData)
                .then(response => {
                    
                    console.log('vote added:', response.data);
                })
                .catch(error => {
                    console.error('Error adding vote:', error);
                });


        },
        addvotes() {
            // this.dialog = false
            //     axios
            //         .post('https://localhost:7050/api/votes', this.formData)
            //         .then(response => {
            //             console.log('VOTES SUBMITTED SUCCESSFULLY:', response.data);
            //         })
            //         .catch(error => {
            //             console.error('ERROR SUBMITTING VOTES:', error);
            //         });
            //     this.dialog = false;

        },
        cancel() {
            this.dialog = false
        }

    },
};
</script>

<style scoped>.logo {
    max-width: 50px;
    max-height: 50px;
    border-radius: 25px;
    margin-left: 20px;
}

.d-none {
    display: none !important;
}</style>
