<template lang="html">

  <b-container class="p-4">
    <b-row>
      <div class="circular ui animated primary button" variant="primary" tabindex="0" id="torankbutton" v-on:click="toranking()">
        <div class="visible content">Ranking</div>
        <div class="hidden content">
          <i class="left arrow icon"></i>
        </div>
      </div>
    </b-row>
    <b-row>
      <b-col>
        <b-row>
          <h2 class="mx-auto" style="width: 166px;"><i class="map icon"></i> Active Trips</h2>
        </b-row>
        <b-row class="form-group">
          <b-form class="w-100">
            <b-form-input v-model="adSearchInput" placeholder="Search" class="my-2"></b-form-input>
            <label for="advertStatusFilter">Status:</label>
            <b-form-select id="advertStatusFilter" :options=tripStatuses v-model="tripStatus" />
          </b-form>
        </b-row>
      </b-col>
      <div class="border-right mx-2" style="width: 1px;" />
      <b-col>
        <b-row>
          <h2 class="mx-auto" style="width: 119px;"><i class="car icon"></i> Drivers</h2>
        </b-row>
        <b-row class="form-group">
          <b-form-input v-model="driverSearchInput" placeholder="Search" class="my-2"></b-form-input>
        </b-row>
      </b-col>
      <div class="border-left mx-2" style="width: 1px;"/>
      <b-col>
        <b-row>
          <h2 class="mx-auto" style="width: 154px">
            <i class="child icon"></i>Passengers</h2>
        </b-row>
        <b-row>
          <b-form-input v-model="passengerSearchInput" placeholder="Search" class="my-2"></b-form-input>
        </b-row>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
        <b-row>
          <b-list-group class="w-100">
            <b-list-group-item class="text-center" v-b-toggle="'advertCollapse' + trip.id" href="#" v-for="trip in filteredTrips" :key="trip.id">
              <span class="font-weight-bold">{{trip.title}}</span>
              <b-collapse accordion="advert-accordion" :id="'advertCollapse'+trip.id">
                <table class="table">
                  <tbody>
                    <tr scope="row">
                      <th>Created by</th>
                      <td>{{trip.driverUsername}}</td>
                    </tr>
                    <tr>
                      <th scope="row">Date and time</th>
                      <td>{{trip.startTime}}</td>
                    </tr>
                    <tr>
                      <th scope="row">Starting at</th>
                      <td>{{trip.startLocation}}</td>
                    </tr>
                    <tr>
                      <th>Ending at</th>
                      <td>{{trip.endLocation}}</td>
                    </tr>
                    <tr>
                      <th>Seats remaining</th>
                      <td>{{trip.seatsAvailable}}</td>
                    </tr>
                    <tr>
                      <th scope="row">Status</th>
                      <td>{{translateTripStatus(trip.tripStatus)}}</td>
                    </tr>
                  </tbody>
                </table>
                <div v-if="trip.vehicle !== null">
                  <span class="font-weight-bold">Vehicle</span>
                  <table class="table">
                    <tbody>
                      <tr>
                        <th scope="row">Model</th>
                        <td>{{trip.vehicle.model}}</td>
                      </tr>
                      <tr>
                        <th scope="row">Colour</th>
                        <td>{{trip.vehicle.color}}</td>
                      </tr>
                      <tr>
                        <th scope="row"># of Seats</th>
                        <td>{{trip.vehicle.maxSeat}}</td>
                      </tr>
                      <tr>
                        <th scope="row">License Plate</th>
                        <td>{{trip.vehicle.licencePlate}}</td>
                      </tr>
                    </tbody>
                  </table>
                </div>
                <span class="font-weight-bold">Stops</span>
                <table class="table">
                  <tbody v-for="stop in trip.stops">
                    <tr>
                      <th scope="row">Location</th>
                      <td>{{stop.stopName}}</td>
                    </tr>
                    <tr>
                      <th scope="row">Price</th>
                      <td>{{stop.price}}</td>
                    </tr>
                  </tbody>
                </table>
              </b-collapse>
            </b-list-group-item>
          </b-list-group>
        </b-row>
      </b-col>
      <div class="border-right mx-2" style="width: 1px;" />
      <!-- <b-col>
        <div class="ui vertical divider">
        </div>
      </b-col> -->
      <b-col>
        <b-row>
          <b-list-group class="w-100">
            <b-list-group-item class="text-center" v-b-toggle="'driverCollapse' + user.id" href="#" v-for="user in filteredDrivers" :key="user.id">
              <div class="font-weight-bold">{{user.username}}</div>
              <b-collapse accordion="driver-accordion" :id="'driverCollapse'+user.id">
                <table class="table">
                  <tbody>
                    <tr>
                      <th scope="row">Driver Status</th>
                      <td>{{user.status}}</td>
                    </tr>
                  </tbody>
                </table>
              </b-collapse>
            </b-list-group-item>
          </b-list-group>
        </b-row>
      </b-col>
      <div class="border-right mx-2" style="width: 1px;" />
      <!-- <b-col>
        <div class="ui vertical divider">
        </div>
      </b-col> -->
      <b-col>
        <b-row>
          <b-list-group class="w-100">
            <b-list-group-item class="text-center" v-b-toggle="'passengerCollapse' + user.id" href="#" v-for="user in filteredPassengers" :key="user.id">
              <div class="font-weight-bold">{{user.username}}</div>
              <b-collapse accordion="passenger-accordion" :id="'passengerCollapse'+user.id">
                <table class="table">
                  <tbody>
                    <tr>
                      <th scope="row">Passenger Status</th>
                      <td>{{user.status}}</td>
                    </tr>
                  </tbody>
                </table>
              </b-collapse>
            </b-list-group-item>
          </b-list-group>
        </b-row>
      </b-col>
    </b-row>
  </b-container>
</template>

<script src="./fleet.js" />

<style lang="css">
</style>
