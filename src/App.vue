<template>
  <div id="app">
    <div class="table-container">
      <h2 class="my-5">Lista de Personas</h2>
      <table class="table">
        <thead>
          <tr>
            <th>Nombre</th>
            <th>Apellido</th>
            <th>Edad</th>
            <th>Altura</th>
            <th>Peso</th>
            <th>Ciudad</th>
            <th>País</th>
            <th>Estudios</th>
            <th>Género</th>
            <th>Grupo Sanguíneo</th>
            <th>Hora Local</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="person in people" :key="person.person_id">
            <td>{{ person.name }}</td>
            <td>{{ person.surname1 }}</td>
            <td>{{ person.age }}</td>
            <td>{{ person.height }}</td>
            <td>{{ person.weight }}</td>
            <td>{{ getCityName(person.city_id) }}</td>
            <td>{{ getCountryName(getCityCountryId(person.city_id)) }}</td>
            <td>{{ getStudyLevel(person.study_id) }}</td>
            <td>{{ getGenderType(person.gender_id) }}</td>
            <td>{{ getBloodTypeName(person.bloodtype_id) }}</td>
            <td>{{ getLocalTime(person.city_id) }}</td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
import { DateTime } from "luxon";

export default {
  name: "App",
  data() {
    return {
      utc: DateTime.utc().toFormat("ttt "),
      value: 0,
      continente: "Europa",
      url: "https://www.google.es/maps/place",
      people: [
        {
          person_id: "1",
          name: "Laurie",
          surname1: "Moreau",
          age: 10,
          height: 130,
          weight: 32,
          city_id: "5",
          study_id: "1",
          gender_id: "2",
          bloodtype_id: "1",
        },
        {
          person_id: "2",
          name: "María",
          surname1: "Martínez",
          age: 40,
          height: 165,
          weight: 55,
          city_id: "2",
          study_id: null,
          gender_id: "2",
          bloodtype_id: "4",
        },
        {
          person_id: "3",
          name: "Akita",
          surname1: "Yamaguchi",
          age: 85,
          height: 160,
          weight: 63,
          city_id: "3",
          study_id: "1",
          gender_id: "1",
          bloodtype_id: "2",
        },
        {
          person_id: "4",
          name: "Javiera",
          surname1: "García",
          age: 25,
          height: 150,
          weight: 70,
          city_id: "1",
          study_id: "2",
          gender_id: "2",
          bloodtype_id: "3",
        },
        {
          person_id: "5",
          name: "Fausta",
          surname1: "Sanz",
          age: 55,
          height: 155,
          weight: 65,
          city_id: "4",
          study_id: null,
          gender_id: "2",
          bloodtype_id: "1",
        },
      ],
      cities: [
        {
          city_id: "1",
          cityName: "Pamplona",
          country_id: "1",
        },
        {
          city_id: "2",
          cityName: "Santa Cruz de Tenerife",
          country_id: "1",
        },
        {
          city_id: "3",
          cityName: "Tokyo",
          country_id: "4",
        },
        {
          city_id: "4",
          cityName: "Bogotá",
          country_id: "3",
        },
        {
          city_id: "5",
          cityName: "Burdeos",
          country_id: "2",
        },
      ],
      countries: [
        {
          country_id: "1",
          countryName: "España",
        },
        {
          country_id: "2",
          countryName: "Francia",
        },
        {
          country_id: "3",
          countryName: "Colombia",
        },
        {
          country_id: "4",
          countryName: "Japón",
        },
      ],
      studies: [
        {
          study_id: "1",
          level: "Universidad",
        },
        {
          study_id: "2",
          level: "Instituto",
        },
      ],
      gender: [
        {
          gender_id: "1",
          type: "Hombre",
        },
        {
          gender_id: "2",
          type: "Mujer",
        },
      ],
      bloodType: [
        {
          bloodType_id: "1",
          bloodName: "A",
        },
        {
          bloodType_id: "2",
          bloodName: "B",
        },
        {
          bloodType_id: "3",
          bloodName: "AB",
        },
        {
          bloodType_id: "4",
          bloodName: "0",
        },
      ],
    };
  },
  methods: {
    getCityName(cityId) {
      const city = this.cities.find((city) => city.city_id === cityId);
      return city ? city.cityName : "";
    },
    getCityCountryId(cityId) {
      const city = this.cities.find((city) => city.city_id === cityId);
      return city ? city.country_id : "";
    },
    getCountryName(countryId) {
      const country = this.countries.find(
        (country) => country.country_id === countryId
      );
      return country ? country.countryName : "";
    },
    getStudyLevel(studyId) {
      const study = this.studies.find((study) => study.study_id === studyId);
      return study ? study.level : "-";
    },
    getGenderType(genderId) {
      const gender = this.gender.find(
        (gender) => gender.gender_id === genderId
      );
      return gender ? gender.type : "";
    },
    getBloodTypeName(bloodTypeId) {
      const bloodType = this.bloodType.find(
        (type) => type.bloodType_id === bloodTypeId
      );
      return bloodType ? bloodType.bloodName : "";
    },
    getIdUtc(id) {
      return this.cities.find((el) => el.city_id == id).utc;
    },
    getLocalTime(id) {
      const Utc = this.getIdUtc(id);
      const hora = DateTime.utc().setZone(Utc).toFormat("HH : mm ");
      return hora;
    },
  },
};
</script>

<style>
/* Agrega estilos aquí si es necesario */
</style>
