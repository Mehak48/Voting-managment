// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract VotingManagementSystem {

    // --- Part 1: Candidate Voting System ---
    struct Candidate {
        uint id;
        string name;
        uint voteCount;
    }

    mapping(uint => Candidate) public candidates;
    uint public candidateCount;

    function addCandidate(string memory _name) public {
        candidateCount++;
        candidates[candidateCount] = Candidate(candidateCount, _name, 0);
    }

    function getCandidate(uint _id) public view returns (string memory, uint) {
        Candidate memory c = candidates[_id];
        return (c.name, c.voteCount);
    }

    // --- Part 2: Admin-controlled Election Management ---
    address public admin;

    constructor() {
        admin = msg.sender;
    }

    modifier onlyAdmin {
        require(admin == msg.sender, "Not Allowed");
        _;
    }

    mapping(string => bool) public isCandidateActive;

    function addCandidates(string memory _candidate) public onlyAdmin {
        isCandidateActive[_candidate] = true;
    }

    function removeCandidates(string memory _candidate) public onlyAdmin {
        isCandidateActive[_candidate] = false;
    }

    bool public votingStarted;

    function startVoting() public onlyAdmin {
        votingStarted = true;
    }

    function endVoting() public onlyAdmin {
        votingStarted = false;
    }

    // --- Part 3: Voter Management ---
    struct Voter {
        bool hasVoted;
        uint votedCandidateId;
    }

    Voter public v1;
    Voter public vote;

    function Register(uint _candidateId) public {
        require(!v1.hasVoted, "You are already registered");
        v1.hasVoted = true;
    }

    function insert(uint _candidateId) public {
        v1.votedCandidateId = _candidateId;
    }

    function Vote() public {
        require(v1.hasVoted, "Voter already voted");
        v1.hasVoted = true;
    }

    function insertCandidate(uint _candidateId) public {
        vote = Voter(true, _candidateId);
    }

    function updateCandidate(uint _candidateId) public {
        vote = Voter(true, _candidateId);
    }

    function delCandidate(uint _candidateId) public {
        vote = Voter(true, _candidateId);
    }
}
